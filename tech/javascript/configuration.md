---
title: Saito-Lite-Rust Configuration
description: Configuration instructions for SLR
published: true
date: 2024-10-16T01:11:01.291Z
tags: 
editor: markdown
dateCreated: 2024-10-16T00:00:13.358Z
---

# Saito-Lite-Rust Configuration

After [installing](/tech/installation/javascript) Saito-Lite-Rust you will be ready to configure the server to run the applications you wish to support and provide them to browsers on-demand. This section covers these follow-on configuration steps.

## Configuration Files

Saito uses two main configuration files. 

- `config/options`
- `config/modules.config.js`

`config/options` specifies network configuration options like the IP address on which the server runs and the ports it should open and the peers to which it should connect. 

`config/modules.config.js` file specifies which modules should run on the server (core) and which modules should be served to any browsers that connect to it (lite).

## Compilation

Compiling produces a compressed version of Saito which will include the modules listed in `modules.config.js` - this compiled Javascript is served to browsers which connect to the server and request the default modules.

There are two primary compilation commands. 

- `npm run nuke`
- `npm run compile`


The more extreme `npm run nuke` will reset the blockchain and is useful for your first installation or for hard resets where your local version of the chain is not important to retain. It will also create fresh versions of these configuration files from template config files stored in the `config` directory.

Use `npm run compile` if you wish to change or update the applications supported and distributed on your server without resetting the blockchain - better for [deployed](https://wiki.saito.io/en/tech/deployment) nodes connected to mainnet.

### Advanced Usage of the `compile` Script

The `compile` script supports additional logging options, which can be specified using the `--loglevel` or `-l` flags. This feature allows you to set the desired log level for the compilation process.

#### Usage:

To set a specific log level, use one of the following commands:

```bash
npm run compile -- --loglevel=<level>
```

or 
```
npm run compile -- -l <level>
```

Where level can be one of the following:

- error
- warn
- info
- trace
- debug
For example, to set the log level to 'warn', you can use either:

```
npm run compile -- --loglevel=warn


or

npm run compile -- -l warn

```

### Javascript Client 'dev' Flag

Both the `compile` and `nuke` scripts can be run with a `dev` flag:

```
npm run compile dev
npm run nuke dev
```

When this flag is used:

 * JavaScript is not minimized and source maps are shipped with the code 
   The payload is 2 to 3 times larger than otherwise but makes in-browser 
   debugging possible.
   
 * CSS files are linked (```@include()``` CSS source files, rather than 
   being a concatentation of the source CSS). This makes CSS development
   slightly easier.
   
The result is that many more files are downloaded by the client, but in-browser debugging is much easier