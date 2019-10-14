#!/bin/bash

IPYNB_FILES=`git diff --staged --name-only | awk "/.ipynb/"`
echo "$IPYNB_FILES"

cd "notebooks"

function get_script_extension() {
     # find file_extension from notebook metadata json, get value from file_extension property
     echo $(awk '/"file_extension": ".*"/{ print $0 }' $1 | cut -d '"' -f4)
}

if [[ -n "$IPYNB_FILES" ]]; then
     for ipynb_file in $IPYNB_FILES
     do
         file_path="${ipynb_file##*/}"
         file_no_extension="${file_path%.*}"

        # if file exists and is not a checkpoint file
         if [[ -f "$file_path" ]] && [[ "$file_path" != *"checkpoint"* ]]; then
             echo "Creating scripts from notebook."
             jupyter nbconvert --to script "$file_path"
             # update scripts file in scripts directory
             extension=$(get_script_extension $file_path)
             mv -f "$file_no_extension$extension" "../scripts"

            echo "Creating html from notebook."
             jupyter nbconvert --to html "$file_path"
             # update html file in scripts directory
             mv -f "$file_no_extension.html" "../html"

            # clear notebook output
             echo "Clearing notebook output."
             jupyter nbconvert --ClearOutputPreprocessor.enabled=True --inplace "$file_no_extension.ipynb"
         fi
     done
fi

# return to root directory
cd ..

# add the newly created files to the current commit
git add -A
