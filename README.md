Sublime Yeoman
===================

A Sublime Text 2 plug-in to allow creating any kind of project from your own custom templates (based on the former [STProjectMaker](https://github.com/bit101/STProjectMaker)). Currently in alpha.

Includes a `.sublime-build` file for running `npm install && bower install` for you once your project has been scaffolded.

![](https://f.cloud.github.com/assets/110953/819687/680e6e5e-efb6-11e2-869a-9ffedfb101e4.jpg)

## Currently includes templates for

* AngularJS
* Backbone
* Ember
* Chrome App
* RequireJS
* WebApp


## Installation

### Manually:

Clone or download this project into a folder named "SublimeYeoman" in your Sublime Text 2 Packages folder. If you're not sure where your Packages folder is, use menu `Preferences/Browse Packages...`

Optionally, set up a key binding. I like to override Control-Shift-N in menu `Preferences/Key Bindings - User`

	[
		{ "keys": ["ctrl+shift+n"], "command": "project_maker" }
	]

## Usage

* Invoking "SublimeYeoman" from the command palette will show a Quick Panel list of available templates.
* Choose the template to base your project on.
* You will be prompted to enter a path for your new project. Do so.
* You may be prompted for values for any replaceable tokens in any template files or file names. Enter the values you want to use.
* Newly created project folder will be opened up in Sublime Text

## Creating and Modifying Templates

A template is simply a folder stored in `<sublime packages dir>/SublimeYeoman/Templates/`. It can contain any number and types of files and nested folders of files.

### Tokens

Text files in the template may contain replaceable tokens in the form of `${{token_name}}`. When you create a new project, you will be prompted for values to use for each token found. The same token can be used multiple times in multiple files. You will only be prompted a single time for its value.

Example:

	Hello from ${{user_name}}

when supplied a value of `Paul` for the `user_name` token will become:

	Hello from Paul

### Tokenized File Names

Template file names may also be tokenized using the form `_token_name_.ext`. The leading underscore, token name and trailing underscore will be replaced by the value given.

Example:

	/foo/bar/baz/_info_file_.text

when supplied with a value of `data` for the `info_file` token will become:

	/foo/bar/baz/data.text


### Predefined Tokens

There are two predefined tokens:

`${{project_path}}` in text files will be replaced by the absolute path of the new project directory.

`${{project_name}}` in text files or `_project_name_` as a file name will be replaced by the base name of the project directory.

Example:

Project path is `/foo/bar/baz/MyProject/`

`project_path` will be replaced by `/foo/bar/baz/MyProject/`

`project_name` will be replaced by `MyProject`

### Sublime Project files

If the chosen template has a `.sublime-project` file in the top level, that file will be copied over and processed like any other file in the template. However, if this does not exist, a default `.sublime-project` file will be created using the `project_name` token as its base name. 

## FAQ

## What are the limitations of the current plugin?

Sublime Yeoman currently ships with samples static templates for a number of different types of projects. These templates are the output of the corresponding Yeoman generators, however we eventually intend on shelling out to the `yo` binary to provide access to all Yeoman community generators.

### How do you ignore files?

You don't want to try to do token replacement in binary files. The plug-in has a long list of file types that it will ignore when doing token replacement. You can always add your own if any files in your templates cause a problem. The list is contained in the `yeoman.sublime-settings` file. Note, these files _will_ be copied into the project. They will just not be parsed for tokens.

