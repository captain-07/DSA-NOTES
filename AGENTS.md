## Custom Command: Compile DSA Notes

When I ask you to "compile DSA notes" or "build NotebookLM file":
1. Recursively search for all `.md` files in the workspace (excluding `AGENTS.md` and `All_DSA_Compiled.txt`).
2. Combine their contents into `All_DSA_Compiled.txt` at the root.
3. Add a clear separator and Markdown header (`# File: <filename>`) before the content of each file.
4. Mention total number of files merged at above.
5. Combine them by the order they have been created. 
6. Notify me when completed with the total file count merged.