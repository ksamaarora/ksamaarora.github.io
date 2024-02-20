---
layout: default
title: Rename Multiple Files
---
> ## Automate Parsing and Renaming of Multiple Files

```bash
import os
# Change Directory if files are located somewhere else
os.chdir('path')
# Display cwd
print(os.getcwd())
```

- Parsing and Renaming Files

```bash
for file_name in os.listdir():

    # Splitting file name and extension
    base_name, file_ext = os.path.splitext(file_name)
    print(base_name)
    # Output: 'example-file-01'

    # Splitting filename into title, course, and number
    title, course, file_num = base_name.split('-')
    print(course)
    # Output: 'file'

    # Stripping whitespaces and zero-padding the number
    title = title.strip()
    course = course.strip()
    file_num = file_num.strip()[1:].zfill(2)

    # Creating a new filename with a standardized format
    new_name = '{}-{}{}'.format(file_num, title, file_ext)
    # Output: '01-examplefile.txt'

    # Renaming the file
    os.rename(file_name, new_name)
```











