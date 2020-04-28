# TokenBridge Burner Wallet 2 Plugin Sample

This sample plugin defines a mediator extension exchange pair to be used in the Exchange Plugin in the burner wallet. 
It uses the resources from the `tokenbridge-plugin` package to define new assets and exchange pairs.

### Clone the sample repo 
Clone the sample repo to create a plugin project that uses the TokenBridge plugin. This sample repo containes a ready to publish plugin for a ERC677 to ERC677 bridge extension, but you can later modify it to define your own resources.

#### Project structure
There are two main folders in the project:
- `wallet` - is a burner wallet instance ready to use your plugin
- `test-wallet` - is a burner wallet instance ready to test your plugin and resources in testnets
- `my-plugin` - is the folder where the plugin code is located. To change the name of the plugin it is necessary to update the folder name `my-plugin` and all mentions to `my-plugin` to the new name of your plugin.

Inside `my-plugin` you can find the files that defines the resources to be exposed by the plugin to be used by the burner wallet in order to interact with the ERC677 to ERC677 bridge extension:
- `Stake` - extends from `ERC677Asset` defined in `tokenbridge-plugin`
- `xStake` - extends from `ERC677Asset` defined in `tokenbridge-plugin`
- `StakeBridge` - extends from `Mediator` defined in `tokenbridge-plugin`

You can extend or replace these resources based on your use case.

### Install dependencies
Run `yarn install`. This repo uses Lerna and Yarn Workspaces, so `yarn install` will install all dependencies and link modules in the repo.

### Build
To build the plugin package, from the root folder of project, you need to run the following command:
```
yarn build
```

### Test plugin and resources in testnets
The project includes a burner wallet instance where you can test the implementation of the plugin in testnet. For that, you have to make sure that the build step was performed and that the plugin resources you modified are correctly imported and used in the `src/index.tsx` file of the `test-wallet` folder.

1. Create `.env` file in `test-wallet` folder from `.env.example` and set the required parameters for the ERC677 to ERC677 bridge extension:
```
REACT_APP_INFURA_KEY=<your key from infura.com>
REACT_APP_HOME_NETWORK=
REACT_APP_HOME_TOKEN_NAME=
REACT_APP_HOME_TOKEN_ADDRESS=
REACT_APP_HOME_MEDIATOR_ADDRESS=

REACT_APP_FOREIGN_NETWORK=
REACT_APP_FOREIGN_TOKEN_NAME=
REACT_APP_FOREIGN_TOKEN_ADDRESS=
REACT_APP_FOREIGN_MEDIATOR_ADDRESS=
```

2. To start the burner wallet instance run:
```
yarn start-test-wallet
```

### Run plugin in Mainnet
The project includes a burner wallet instance where you can use the implementation of the plugin. For that, you have to make sure that the build step was performed and that the plugin resources you modified are correctly imported and used in the `src/index.tsx` file of the `wallet` folder.

1. Create `.env` file in `wallet` folder and set:
```
REACT_APP_INFURA_KEY=<your key from infura.com>
```

2. To start the burner wallet instances run:
```
yarn start-wallet
```

### Publish to npm
In order to make the plugin accessible it needs to be published in the npm registry. For that, you can follow these steps:

1. Create account in https://www.npmjs.com/

2. Go to `my-plugin` folder

3. Run `yarn build`. Make sure it generates the `dist` folder

4. Update `version` in `my-plugin/package.json`

5. Run `yarn publish` and fill login information if required.
The prompt will ask for the new version, complete it with the version from `my-plugin/package.json`


More information in https://classic.yarnpkg.com/en/docs/publishing-a-package/
