---
cssclasses: 
tags:
  - IA
  - ongoing
  - fabric
  - "#bash"
date: 2025-02-19T15:10:00
---
## Description:

Uno script che accetta due argomenti, il primo è il link youtube, il secondo un fisso "cleanup".
Se passato il secondo rimuove il file temporaneo del transcript youtube.
Al momento utilizza tre pattern di #fabric , -y , improve_writing ed extract_wisdom.


## Code:
```
#!/bin/bash

if [ $# -eq 0 ]; then
    echo "Usage: $0 <YouTube link> [cleanup]"
    echo "  - YouTube link: Required. The URL of the YouTube video."
    echo "  - cleanup: Optional. If provided, removes the temporary transcript file."
    exit 1
fi

youtube_link="$1"

# Create a temporary file with a .txt extension
temp_file=$(mktemp --suffix=.txt)

# Run the first fabric command and save output to the temporary file
fabric -y "$youtube_link" --transcript > "$temp_file" && echo "Transcript downloaded"

# Run the improve_writing command using the temporary file as input
fabric --pattern improve_writing < "$temp_file" > improved_transcript.txt && echo "Writing improved"

# Run the extract_wisdom command using the improved transcript as input
fabric --pattern extract_wisdom < "$temp_file" > output.txt && echo "Wisdom extracted"

# Check if the second argument is "cleanup"
if [ "$2" = "cleanup" ]; then
    rm "$temp_file" improved_transcript.txt
    echo "Temporary files removed."
else
    # Save the temporary file as a definitive file
    mv "$temp_file" "full_transcript.txt"
    echo "Full transcript saved as: full_transcript.txt"
    echo "Improved transcript saved as: improved_transcript.txt"
fi

```
---
# References
