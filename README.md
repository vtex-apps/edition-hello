# Hello Editions #

A quick setup for an edition app in VTEX.

### Getting Started ###

#### Clone ####

To clone this repository simply run `vtex init` and choose the `edition app` option.

If you don't have `vtex` toolbelt installed, you can also clone it manually:

```
$ git clone https://github.com/vtex/edition-hello edition-hello
$ cd edition-hello
```

#### Manifest definition ####

After that, you need to, in the `manifest.json`:
 - Change the `vendor` and `name` to your preferred choice
   - By convention, we name any edition app with an `edition-` prefix, like `edition-hello` or `edition-global`
 - Set the appropriate parent edition in the `dependencies` field (must be published by the vendor's sponsor)

#### Adding apps for sub-accounts ####

Then, you can specify apps to be installed in the sub-accounts that have this edition configured.
You do that through the `edition/apps.json` file, adding an entry to the object under the `apps` key
in the format:

```
    "<vendor>.<name>": {
      "major": <desired major>,
      "settings": <initial settings>
    }
```

The settings are optional and can be omitted, but they will define the initial settings that should be
configured for the app when it is installed through the current edition.

e.g.: The contents of the `apps.json` file could be:
```
{
  "apps": {
    "vtex.node-getting-started": { "major": 0 }
  }
}
```

#### Testing ####

Be sure to have [VTEX's toolbelt](https://github.com/vtex/toolbelt)
installed.

Edition apps are not link-able, so to test you have to launch a pre-release versions and set them
on test accounts or workspaces for validation. To do so:
 - Launch a pre-release of your edition: `vtex release patch beta`
 - Check the edition of current account/workspace: `vtex edition`
 - Set the edition in current account/workspace: `vtex edition set <edition>@<version>`
   - All the apps configured in the `apps.json` file will be automatically installed in that
   workspace where the edition was set. You can validate that by inspecting the `vtex ls`
   command output.