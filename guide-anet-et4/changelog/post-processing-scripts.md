# Post-Processing Scripts¶

[Mode](/broken/pages/246b4d07eed07a8ac878abc4613a350fbce2c022): `Advanced`.\
[Variable](/broken/pages/2ce6fff32f5448d0159c2e2dfbcb54f26d3c6918): `post_process`.\
[Type](/broken/pages/726477a877bf7a8efe103413c86723285f8ca2eb#list-types): `Text list`.\
[CLI Example](/broken/pages/f439233018f603f29dcf6b1fcc75b0ab21b6fd24#setting-overrides): `--post-process=value`.\
Here you can set up post-processing scripts that run on the generated G-code.\
For Bambu Lab printers, they run right after slicing, so the preview shows the processed G-code. For other printers, they run only when a G-code file is exported or sent to a network printer with **Print** or **Send**, so the preview and sliced 3MF files keep the unprocessed G-code.\
This allows you to modify the G-code output or perform additional tasks.

Check the script's documentation for dependencies, available parameters and usage instructions.

Example Python script:

```
"C:\Your\Path\To\Python\python.exe" "C:\Your\Path\To\Script\pythonScript.py" -parameterToScript 1994;
```
