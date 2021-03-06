# On Release Process

The `nrwl/nx` and `nrwl/schematics` packages are released together. You must use the same version of the two packages.

# 0.6.13

## Bug Fixes

* [Avoid relative paths to node modules](https://github.com/nrwl/nx/commit/2c49c3029535a9b98216d367e9c2b77a8d40a4a4)
* [Handle the case when libraries are placed in the directory with the same name as an app](https://github.com/nrwl/nx/commit/f862ed05d18e1474156779ad1dee2e7a7c785d1d)

# 0.6.10

## Features

* [Improve error messages in the affected: and format: commands](https://github.com/nrwl/nx/commit/878784ae814ffea28796f458ff2f8b0b641996c0)

## Bug Fixes

* [Handle circular deps between apps and libs](https://github.com/nrwl/nx/commit/3531323fb5210b995b1296a198c8e76ee8bf9a07)
* [Handle projects that have similar names](https://github.com/nrwl/nx/commit/fe7032d29f4dcd66b51dbb889a1cf1751cd1d20a) 
* [Update workspace to set $schema and app name](https://github.com/nrwl/nx/commit/df5bd089b6515ea747f891bf590b46a4e00d0a92) 
* [Update workspace to copy the cli file](https://github.com/nrwl/nx/commit/ddd8de3813f374a752b0e6f47deaa58c2e9f40c8) 
* [Disallow importing apps](https://github.com/nrwl/nx/commit/912fc81708d381f49950255eeff746a2dfd46c7b) 

# 0.6.5

## Features

This release adds the following commands:

```
npm run format:write -- SHA1 SHA2
npm run format:check -- SHA1 SHA2
```

The `format:check` command checks that the files touched between the given SHAs are formatted properly, and `format:write` formats them.

Instead of passing the two SHAs, you can also pass the list of files, like this:

```
npm run format:write -- --files="libs/mylib/index.ts,libs/mylib2/index.ts"
npm run format:check -- --files="libs/mylib/index.ts,libs/mylib2/index.ts"
```

You can add `--libs-and-apps` flag to always run the formatter on apps and libs instead of individual files. 

```
npm run format:write -- SHA1 SHA2 --libs-and-apps
npm run format:check -- SHA1 SHA2 --libs-and-apps
```

Finally, you can the command on the whole repo, like this:

```
npm run format:write
npm run format:check
```

* [Add format:check and format:write commands](https://github.com/nrwl/nx/commit/826a0b1056f9000425e189bad5a5d63966c3a704)


## Bug Fixes

* [Only allow importing libs using the configured npm scope](https://github.com/nrwl/nx/commit/c836668541532e64db088ef9a984678022abb3bd)



# 0.6.0

## Features

This release adds the following commands:

```
npm run apps:affected -- SHA1 SHA2
npm run build:affected -- SHA1 SHA2
npm run e2e:affected -- SHA1 SHA2
```

The `apps:affected` prints the apps that are affected by the commits between the given SHAs. The `build:affected` builds them, and `e2e:affected` runs their e2e tests. 

To be able to do that, Nx analyzes your monorepo to figure out the dependency graph or your libs and apps. Next, it looks at the files touched by the commits to figure out what apps and libs they belong to. Finally, it uses all this information to generate the list of apps that can be affected by the commits. 

Instead of passing the two SHAs, you can also pass the list of files, like this:

```
npm run apps:affected -- --files="libs/mylib/index.ts,libs/mylib2/index.ts"
npm run build:affected ----files="libs/mylib/index.ts,libs/mylib2/index.ts"
npm run e2e:affected ----files="libs/mylib/index.ts,libs/mylib2/index.ts"
```




* [Add support for building and testing only the apps affected by a commit](https://github.com/nrwl/nx/commit/428762664acc5fd155dd7be630dab09101d23542)

## Bug Fixes

* [Make deep import check work for libs with same prefix](https://github.com/nrwl/nx/commit/3c55f34ca12a4d5338099586ffe9455c81a3b199)


# 0.5.3

`ng new myproj --collection=@nrwl/schematics` creates a new workspace. 

For this to work `@nrwl/schematics` and `@angular/cli` have to be installed globally, and they have to be compatible. This is error prone, and it often results in hard to debug errors. And it is impossible for Nx to solve this problem because we do not control your globally installed npm modules. 

That is why we provided a way to create a new workspace using a sandbox that does not depend on any global modules, like this:

```
curl -fsSL https://raw.githubusercontent.com/nrwl/nx/master/packages/install/install.sh | bash -s myprojectname
```

This works, but with one caveat: you have to have `curl` and `bash` installed, which might be a problem for a lot of windows folks. That is why starting with `0.5.3`, `@nrwl/schematics` ships with a binary that works on all platforms and creates an Nx workspace without relying on globally installed npm modules.

This is what you can do now:

```
yarn global add @nrwl/schematics # do it once
create-nx-workspace myproj
```

Some folks also reported having problems running Nx behind a firewall, in a corporate environment. We fixed them as well.


## Features

* [Replace install.sh with a more robust way of creating projects](https://github.com/nrwl/nx/commit/f91b5309bdaf764e436bd544ec4f10c84b99cb08)
* [Bump up the version of prettier](https://github.com/nrwl/nx/commit/1481d169bbb7f1fbe3df5af2bce51c4215776d93)

## Bug Fixes

* [Generate an angular-cli config without the apps array, so the CLI can error properly](https://github.com/nrwl/nx/commit/a7f06edf5914212bcefbafb1198d262e9692cfdb)

# 0.5.2

## Bug Fixes

* [Remove default prop for viewEncapsulation option flag](https://github.com/nrwl/nx/commit/b46eb1c699dd509f4be103979a5938c3f7486fb1)
* [Fix NPM link in README](https://github.com/nrwl/nx/commit/4aa42e4772522a20df384ab9a48861a8d4f7ab0f)
* [Change rxjs version to use hat](https://github.com/nrwl/nx/commit/3b1942ed830ea31269a1fb9e995efb93b182870a)

# 0.5.1

## Features

* [Disable typescript mismatch warnings](https://github.com/nrwl/nx/commit/ecb87a0dcd08f0968d77508976ce43a84f049743)

## Bug Fixes

* ["ng test" should not compile e2e tests](https://github.com/nrwl/nx/commit/ac53e9a624b01cf71f88eb412678ffc48125ff38)
* [Fix 'npm run format'](https://github.com/nrwl/nx/commit/670cd57dfa7d5bbf6b9af4e52f2c7d40081138cb)

# 0.5.0

## Features

* [Update the workspace to use Angular 5.1 and CLI 1.6](https://github.com/nrwl/nx/commit/a477bb9fc953e3b44d696945cc259119f701fb78)

# 0.4.0

## Features

* [Add support for generating nested apps and libs](https://github.com/nrwl/nx/commit/013a828d1e31f55a9b3f7c69587316890ea834d4)
* [Update NgRx schematic to allow the customization of the state folder](https://github.com/nrwl/nx/commit/a2d02652665f497be8958efc403d7a44bd831088)

## Bug Fixes
 
* [Only begin converting to workspace once files have been checked](https://github.com/nrwl/nx/commit/e7fd6b1e04f3f3387a91c53a7ac479fe72bdd72e)
* ["ng build" should only recompile the selected app](https://github.com/nrwl/nx/commit/550de7bb80f4d3f306c23fac70db52c98dadcd05)

## Refactoring

* [Eliminated single letter variable names in effects template](https://github.com/nrwl/nx/commit/996143cf60bac1a57629815d5756db9ce23193ab)

# 0.3.0

We want to be able to add new features to Nx without breaking existing workspaces. Say, you created an Nx Workspace using Nx 0.2.0. Then, half a year later, you decided to upgrade the version of Nx to 0.5.0. Imagine the 0.5.0 release requires you to have more information in your `.angular-cli.json`. Until now, you would have to manually go through the changelog and modify your `.angular-cli.json`. This release adds the `nx-migrate` command that does it for you. Run `npm run nx-migrate` after upgrading `@nrwl/schematics`, and it will upgrade your workspace to be 0.5.0 compatible. 

## Features

* [add `allow` option to whitelist deep imports](https://github.com/nrwl/nx/commit/b3f67351fe8890e06402672e687b1789f279613b)
* [Added the nx-migrate command](https://github.com/nrwl/nx/commit/d6e66b99316181b8b67805b91cc35457c3465029)
* [Upgrade Prettier to 1.8.2](https://github.com/nrwl/nx/commit/cc2277e91be2ca49fb1588f1d8e29ef91fd12044)
* [Update readme to point to example apps using Nx](https://github.com/nrwl/nx/commit/3d53e31391d5d79a0724d099c7121edb53e8b163)

# 0.2.2

## Bug Fixes

* [Adds a schema file to allow custom properties that the default CLI distribution does not support](https://github.com/nrwl/nx/commit/7fd7594e673cf38af7668b891ed7c75b390b3330)
* [Fix issue with generating a wrong full path on windows](https://github.com/nrwl/nx/commit/11e6c055ba1211a5bee1cc73d46663985645f08e)

# 0.2.1

## New Features

* [Export jasmine-marbles getTestScheduler and time functions](https://github.com/nrwl/nx/commit/2e4613f475fc2673731540fb4724d6ba2af02aae)
* [Use fetch instead of optimisticUpdate in the generated effect classes](https://github.com/nrwl/nx/commit/c9759cc4427283422e906ed19a8a2dabcb2a656b)

## Bug Fixes

* [--routing should add RouterTestingModule](https://github.com/nrwl/nx/commit/d7fc5b56054c9a4c1fbb12845bfc0803f9a9ff86)
* [Fix wording in the documentation](https://github.com/nrwl/nx/commit/058c8995f35a9e677f88404bc9c8a2b177487080)

## Refactorings

* [Refactor Nx to use RxJS lettable operators](https://github.com/nrwl/nx/commit/715efa4b225b65be0052a1e6a88c5bdcd5a6cf38)

# 0.2.0

## New Features

### Changing Default Library Type

We changed the default library type from "simple" to "Angular". So where previously you would run:

```
ng generate lib mylib // simple TS library
ng generate lib mylib --ngmodule // an angular library
```

Now, you run:

```
ng generate lib mylib // an angular library
ng generate lib mylib --nomodule // simple ts library
```

### Generating Router Configuration

You can pass `--routing` when generating an app.

```
ng generate app myapp --routing // generate an angular app with router config
```

The generated app will have `RouterModule.forRoot` configured.

You can also pass it when generating a library, like this:

```
ng generate lib mylib --routing
```

This will set up the router module and will create an array of routes, which can be plugged into the parent module. This configuration works well for modules that aren't loaded lazily.

You can add the `--lazy` to generate a library that is loaded lazily.

```
ng generate lib mylib --routing --lazy
```

This will also register the generated library in tslint.json, so the linters will make sure the library is not loaded lazily.

Finally, you can pass `--parentModule` and the schematic will wire up the generated library in the parent router configuration.

```
ng generate lib mylib --routing --parentModule=apps/myapp/src/myapp.module.ts
ng generate lib mylib --routing --lazy --parentModule=apps/myapp/src/myapp.module.ts
```

