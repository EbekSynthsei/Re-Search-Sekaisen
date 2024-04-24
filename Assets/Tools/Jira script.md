#!/bin/bash

usage() {
	echo "
Usage: wti [-h?] [-l LOGIN] ISSUE...

wti = \"(W)hat (T)he (I)ssue?\". Script tries to get description of the specified 
ISSUE(es) from jira. For each ISSUE in list script will ouput the line in 
the following format: ISSUE_ID — ISSUE_DESC

options:

 -h -?	Print this message and exit

 -l	LOGIN	Jira-user login. Will be promted if not specified."
}

shortusage() {
	echo "
Usage: wti [-h?] [-l LOGIN] ISSUE...

See wti -h for help"
}

error() {
	if [[ -n $1 ]];
	then
		echo -e "\nERROR: $1"
		if [[ -n $2 ]];
		then
			shortusage
		fi
		exit 1
	fi	
}

JIRA_URL="https://jira.atlassian.com"
JIRA_AUTH_URI="/rest/auth/latest/session"
JIRA_API_URI="/rest/api/latest/"

OPTIND=1

# Parsing flags
while getopts "h?l:" opt
do
	case $opt in
		h|\?)
			usage
			exit 0
			;;
		l)
			JIRA_LOGIN=$OPTARG
			;;
	esac
done

# getting list of braches
if [[ -z ${!OPTIND} ]]; then
	error "You must specified at least one issue!" 1
else
	for ((ARG=$OPTIND, NUM=0; ARG>0; ARG++));
	do
		if [[ -z ${!ARG} ]];
		then
			break
		fi
		ISSUES[$NUM]=${!ARG}
		NUM=$[NUM+1]
	done
fi

# getting login fo JIRA
if [[ -z $JIRA_LOGIN ]]; then
	read -p "Enter your login for JIRA: " JIRA_LOGIN
fi
# getting password for JIRA
read -sp "Enter your password for JIRA: " JIRA_PASSWORD
echo ""

# authentication in JIRA
JIRA_SESSION_ID=`curl -s -H "Content-Type: application/json" -d "{\"username\":\"${JIRA_LOGIN}\",\"password\":\"${JIRA_PASSWORD}\"}" -X POST ${JIRA_URL}${JIRA_AUTH_URI} | sed -r 's/^.+JSESSIONID","value":"([^"]+).+$/\1/ig'`

if [[ -n $(echo $JIRA_SESSION_ID | grep error) ]]
then
	error "Wrong login or password!"
fi

# getting info about branches
for ((I=0; I<${#ISSUES[@]}; I++));
do
	SED=`curl -s -H "Content-Type: application/json" -b JSESSIONID=${JIRA_SESSION_ID} ${JIRA_URL}${JIRA_API_URI}issue/${ISSUES[$I]}?fields=summary | sed -n -re 's@\\\["]([^\\\]+)\\\["]@«\1»@ig' -e 's/^.+key":"([^"]+)".+summary":"([^"]+).+$/\1 - \2\n/igp'`
	if [[ -z $SED ]]
	then
		echo "Issue \"${ISSUES[$I]}\" not found or unknown error has occured!"
	else
		echo $SED
	fi
done