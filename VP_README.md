# Vox Pupuli PDK Templates
This is a fork of the pdk-templates from Puppet intended for Vox Pupuli Organization.  Since Vox Pupuli has different workflows and automations we require slightly different templates than the upstream.  We will strive to keep the changes to a minimum but over time these changes may drift. 

## Testing Template changes
You can test pdk-template changes locally by running `pdk convert` in a module that uses pdk.

This will tell pdk to use the local templates and consequently update the metadata.json file as well.

Example:

```shell
git clone https://github.com/voxpupuli/pdk-templates /voxpupuli/pdk-templates
git clone https://github.com/voxpupuli/puppet-format.git
cd puppet-format
pdk convert --template-url=/voxpupuli/pdk-templates --template-ref=vp-1.18.0
----------Files to be modified----------
/voxpupuli/modules/puppet-format/metadata.json

----------------------------------------

You can find a report of differences in update_report.txt.

Do you want to continue and make these changes to your module? Yes

------------Update completed------------

1 files modified.

View the changes and validate within the puppet module that those changes work.

pdk validate
pdk test
```

When finished testing you will need to convert back to the github hosted pdk-templates.

`pdk convert --template-url=https://github.com/voxpupuli/pdk-templates --template-ref=vp-1.18.0`

## Updating templates
When updating templates we try and keep as close to the upstream source as possible.  To do this you must perform the 
following steps.

1. git clone https://github.com/voxpupuli/pdk-templates /voxpupuli/pdk-templates
2. cd /voxpupuli/pdk-templates
3. git remote add upstream https://github.com/puppetlabs/pdk-templates
4. git fetch upstream
5. git checkout vp-1.x.x (latest version) ie. `git checkout vp-1.17.0`
6. git rebase 1.18.0 (latest tag from upstream )
7. Resolve any conflicts during rebase
8. Test changes locally before pushing branch (see steps about testing locally)
9. Once you have verified updates have worked, you can push the new branch ie. git push origin vp-1.18.0

Note: Since we have modified the original pdk templates we prepend a `vp-` in front of the tag to designate these our Voxpupuli changes.

I don't know how sustainable this workflow is so comments or suggestions are welcomed. 

## Converting a module
Converting your module to use Vox Pupuli's version of pdk-templates is easy as:

`pdk convert --template-url=https://github.com/voxpupuli/pdk-templates --template-ref=vp-1.18.0`

While the version may change over time the procedure is the same.

Please be aware that if you have something custom in any of the files that pdk manages you will need to create a .sync.yml file and keep the changes there.  Please see https://github.com/voxpupuli/pdk-templates#basic-usage for more info.

