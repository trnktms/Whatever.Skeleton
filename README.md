# sk-base - the project generator with PowerShell

### Purpose of the project
Accelarate whatever project initial setup, project and module addition included with common needs.

### How to use your own template, configuration with your project
Download this repository and put it into your own project, so your folder structure would look like this for instance:
- `sk-base`
    - `sk-configs`
    - `sk-queue`
    - `sk-scripts`
- `sk-configs` - JSON configuration folder for your templates
- `sk-templates` - template folder
    - `add-module`
        - `your-module-template-1`
        - `your-module-template-2`
        - `...`
    - `add-project`
        - `your-project-template-1`
        - `your-project-template-2`
        - `...`
    - `init`
        - `your-init-template-1`
        - `your-init-template-2`
        - `...`
- `target` - the place where the generated files goes

Just use the following parameters when you call `init.ps1` or `add-project.ps1` or `add-module.ps1` optionally:
- `configPath`
- `templatePath`
- `targetPath`

### Commands
#### init.ps1
 1. Run the `init.ps1` PowerShell script from the `sk-scripts` folder, which sets up your solution based on `default.config.json` by default. Here is an example how the config could look like:
```
{
    "projectName": "MyProject",
    "targetFramework": "v4.6.2",
    "nugetTargetFramework": "net462",
    "aspNet": {
        "lib": "net45",
        "mvcVersion": "5.2.3",
        "webPagesVersion": "3.2.3",
        "razorVersion": "3.2.3"
    },
    "[guid]" : {
        "type" : "guid",
        "format": "D"
    },
    "[[subProjectId]]" : {
        "type" : "guid",
        "format" : "D"
    }
}
```

#### add-project.ps1
 1. Run the `add-project.ps1` command with 2 required parameters:
    - `subProjectName`: name of the new project (e.g. `Navigation`)
    - `templateName`: name of the subfolder from `.\sk-templates` (`your-project-template-1` or `your-project-template-2`)
 2. This command uses the same `default.config.json` config above

#### add-module.ps1
 1. Run the `add-module.ps1` command with 3 required parameters:
    - `moduleName`: name of the new module (e.g. `TextModule`)
    - `subProjectName`: name of the new project (e.g. `Navigation`)
    - `templateName`: name of the subfolder from `.\sk-templates\default` (`your-module-template-1` or `your-module-template-2`)
 2. This command uses the same `default.config.json` config above

### How to create your own templates and configurations

#### Configuration
You can create your own configuration with the same parameter names or you can even create your custom parameters.
Only the `projectName` is a hardcoded and required parameter name but the others can be removed and changed.

#### Template
You can create your own templates (different, less complex or more complex), you just need to follow the following placeholder name convention:
- One level deep parameter: `[<parameterName>]` e.g. `[nugetTargetFramework]`
- Two or more level deep: `[<firstLevel>.<secondLevel>]` e.g. `[aspNet.lib]`
- `[guid]`: unique GUID generation in all places where it is used
- `[[subProjectId]]`: one-time GUID generation, so the same generated GUID is used in all places

**Important: your JSON configuration should be in sync with your template!**