{
    "git.ignoreMissingGitWarning": true,
    "workbench.colorTheme": "Default Dark+",
    
    //"latexCompile.compiler": "xelatex",
    "latex-workshop.latex.recipes": [
        {
            "name": "xelatex",
            "tools": [
                "xelatex"
            ]
        }
    ],
    "latex-workshop.latex.tools": [
    {
        "name": "xelatex",
        "command": "xelatex",
        "args": [
        "-synctex=1",
        "-interaction=nonstopmode",
        "-file-line-error",
        "%DOCFILE%"
        ]
    }, 
    {
        "name": "bibtex",
        "command": "bibtex",
        "args": [
            "%DOCFILE%"
        ]
    }, 
    {
        "command": "xelatex",
            "args": [
            "-synctex=1",
            "-interaction=nonstopmode",
            "-file-line-error",
            "%DOCFILE%"
            ]
    }, 
    {
        "name": "xelatex",
        "command": "xelatex",
        "args": [
        "-synctex=1",
        "-interaction=nonstopmode",
        "-file-line-error",
        "%DOCFILE%"
        ]
    }
  ],
    "window.zoomLevel": 0,
    "latex-workshop.view.pdf.viewer": "tab",
  "editor.fontSize": 16,
  "editor.tabCompletion": "on",
  "editor.tabSize": 2,
  
  }
  