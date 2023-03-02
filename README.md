# Amplify Override Helpers

This is a simple utility to override the DataSource of a custom resolver that is placed is slotted in. 

Amplify currently provides a simple way to override the entire model but overriding a single resolver is not so straightforward. 


## Usage


1. Execute `amplify override api`
2. Copy `amplify-override-helpers.ts` to `amplify\backend\api\YourApi\`
3. Update `amplify\backend\api\YourApi\override.api` as shown below.




```ts


import { AmplifyApiGraphQlResourceStackTemplate } from '@aws-amplify/cli-extensibility-helper';
import { overrideDataSourceByFileName } from './amplify-override-helpers';    // <<== the helper file in this repo

export const override = (resources: AmplifyApiGraphQlResourceStackTemplate) => {

    overrideDataSourceByFileName(
        resources,
        'Mutation.createComment.postUpdate.1', // <== The name of your file (without the extension)
        'Comment',                             // <== The model that this resolver falls within
        'PostTable'                            // <== The new datasource that you want to use
    );
    
    overrideDataSourceByFileName(
        resources,
        'Query.getComment.postDataLoad.1',
        'Comment',
        'PostTable'
    );

};


```


## Notice

Updating the DataSource of an individual resolver is not officially documented so this could break with future updates of Amplify. (In that case, the exceptions should be triggered alerting you and stopping the build process so that you can make changes.)

If this is a feature that you would like the Amplify team to official support please let them know using the appropriate channels. 
