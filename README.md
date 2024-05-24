This repository was initially created as an handout for my presentation at the [Wir sind Ohana 2024](https://www.wirsindohana.de) event in 2024.
I would love to see this repository grow and become a valuable resource for everyone who is working with the Salesforce (Translation) Metadata API.

In this file you can find different examples of how to use the `package.xml` file to retrieve metadata from Salesforce especiall in relation to translations.
You can copy the examples and adjust them to your needs.

Additionally, you can find the corresponding commands to retrieve the metadata using the Salesforce CLI.

Feel free to clone this repository and/or contribute to it. If you have any questions, feel free to reach out to me.

# Table of Contents

1. [Basics](#basics)
6. [Types](#types)
2. [Scripts](#scripts)

## Basics <a name="basics"></a>

### Retrieve
```bash
sf project retrieve start --manifest package.xml
```

### Deploy
```bash
sf project deploy start --manifest package.xml
```

### Package.xml Structure
```XML
<?xml version="1.0" encoding="UTF-8"?>
<Package xmlns="http://soap.sforce.com/2006/04/metadata">
    <version>60.0</version>
</Package>
```

## Types <a name="types"></a>
### Custom Objects

```XML
<?xml version="1.0" encoding="UTF-8"?>
<Package xmlns="http://soap.sforce.com/2006/04/metadata">
    <types>
        <members>Payment__c-de</members>
        <name>CustomObjectTranslation</name>
    </types>
    <version>60.0</version>
</Package>
```

```bash
sf project retrieve start -m "CustomObjectTranslation:Payment__c-de"
```

### Custom Fields
```XML
<?xml version="1.0" encoding="UTF-8"?>
<Package xmlns="http://soap.sforce.com/2006/04/metadata">
    <types>
        <members>Payment__c-de</members>
        <name>CustomObjectTranslation</name>
    </types>
    <types>
        <members>Payment__c.From__c</members>
        <name>CustomField</name>
    </types>
    <version>60.0</version>
</Package>
```
```bash
sf project retrieve start -m "CustomObjectTranslation:Payment__c-de" -m "CustomField:Payment__c.From__c"
sf project retrieve start -m "CustomObjectTranslation:Payment__c-de,CustomField:Payment__c.*"
```

### Standard Picklist (specific)
```XML
<?xml version="1.0" encoding="UTF-8"?>
<Package xmlns="http://soap.sforce.com/2006/04/metadata">
    <types>
        <members>Industry-de</members>
        <name>StandardValueSetTranslation</name>
    </types>
    <version>60.0</version>
</Package>
```
```bash
# Get a specific Standard Picklist Translations for German
sf project retrieve start -m "StandardValueSetTranslation:Industry-de"
```

### Standard Picklist (all)
```XML
<?xml version="1.0" encoding="UTF-8"?>
<Package xmlns="http://soap.sforce.com/2006/04/metadata">
    <types>
        <members>*</members>
        <name>StandardValueSetTranslation</name>
    </types>
    <version>60.0</version>
</Package>
```
```bash
# Get all Standard Picklist Translations for German
sf project retrieve start -m "StandardValueSetTranslation:*-de"
```
### Custom Picklists
Custom Picklists are handled like Custom Fields.

```XML
<?xml version="1.0" encoding="UTF-8"?>
<Package xmlns="http://soap.sforce.com/2006/04/metadata">
    <types>
        <members>Payment__c-de</members>
        <name>CustomObjectTranslation</name>
    </types>
    <types>
        <members>Payment__c.Status__c</members>
        <name>CustomField</name>
    </types>
    <version>60.0</version>
</Package>
```

```XML
<?xml version="1.0" encoding="UTF-8"?>
<Package xmlns="http://soap.sforce.com/2006/04/metadata">
    <types>
        <fullName>Payment__c-de</fullName>
        <name>CustomFieldTranslation</name>
    </types>
    <version>60.0</version>
</Package>
```

### Global Picklist (all)
```XML
<?xml version="1.0" encoding="UTF-8"?>
<Package xmlns="http://soap.sforce.com/2006/04/metadata">
        <types>
        <members>*</members>
        <name>GlobalValueSetTranslation</name>
    </types>
    <version>60.0</version>
</Package>
```
```bash
# Get all Global Picklist Value Translations for German
sf project retrieve start -m "GlobalValueSetTranslation:*-de"
```
### Global Picklist (specific)
```XML
<?xml version="1.0" encoding="UTF-8"?>
<Package xmlns="http://soap.sforce.com/2006/04/metadata">
        <types>
        <members>Numbers-fr</members>
        <name>GlobalValueSetTranslation</name>
    </types>
    <version>60.0</version>
</Package>
```
```bash
# Get all Global Picklist Value Translations for French
sf project retrieve start -m "GlobalValueSetTranslation:Nubmers-fr"
```

### Custem Labels (specific)
```XML
<?xml version="1.0" encoding="UTF-8"?>
<Package xmlns="http://soap.sforce.com/2006/04/metadata">
    <types>
        <members>PaymentMethod</members> <!-- Custom Label Name -->
        <name>CustomLabel</name> <!-- Metadata Type for Custom Labels -->
    </types>
    <types>
        <members>de</members> <!-- German Language Code -->
        <name>Translations</name> <!-- Metadata Type for Translations -->
    </types>
    <version>60.0</version>
</Package>
```

### Flows

Important!
https://developer.salesforce.com/docs/atlas.en-us.api_meta.meta/api_meta/meta_visual_workflow.htm#md_flow_upgrade

```XML
<?xml version="1.0" encoding="UTF-8"?>
<Package xmlns="http://soap.sforce.com/2006/04/metadata">
    <types>
        <members>FlowOne</members> <!-- Custom Label Name -->
        <name>Flow</name> <!-- Metadata Type for Custom Labels -->
    </types>
    <types>
        <members>de</members> <!-- German Language Code -->
        <name>Translations</name> <!-- Metadata Type for Translations -->
    </types>
    <version>60.0</version>
</Package>
```

### Quick Actions
```XML
<?xml version="1.0" encoding="UTF-8"?>
<Package xmlns="http://soap.sforce.com/2006/04/metadata">
    <types>
        <members>New_Record</members>
        <name>QuickAction</name>
    </types>
    <types>
        <members>de</members>
        <name>Translations</name>
    </types>
    <version>60.0</version>
</Package>
```
```bash
sf project retrieve start -m "QuickAction:New_Record" -m "Translations:de"
```

### Custom Tabs (Specific)
```XML
<?xml version="1.0" encoding="UTF-8"?>
<Package xmlns="http://soap.sforce.com/2006/04/metadata">
    <types>
        <members>Web_Tab_Example</members>
        <name>CustomTab</name>
    </types>
    <types>
        <members>de</members>
        <name>Translations</name>
    </types>
    
    <version>60.0</version>
</Package>
```
### Custom Tabs (All)
```XML
<?xml version="1.0" encoding="UTF-8"?>
<Package xmlns="http://soap.sforce.com/2006/04/metadata">
    <types>
        <members>*</members>
        <name>CustomTab</name>
    </types>
    <types>
        <members>de</members>
        <name>Translations</name>
    </types>
    
    <version>60.0</version>
</Package>
```

```bash
sf project retrieve start -m "CustomTab:Web_Tab_Example" -m "Translations:de"
sf project retrieve start -m "CustomTab:*" -m "Translations:de"
```

## Scripts <a name="scripts"></a>

### Get all Translation languages 
```bash
sf org list metadata --metadata-type Translations | jq -r '.[].fullName'
```

### Get all Metadata and retrieve the fullName

```bash
sf org list metadata --metadata-type CustomObjectTranslation | jq -r '.[].fullName' | sort
```

```bash
#!/bin/bash

# Extract fullName attributes from JSON output
fullNames=$(sf org list metadata --metadata-type CustomObjectTranslation | jq -r '.[].fullName' | sort)


# Create or overwrite package.xml
echo "<?xml version=\"1.0\" encoding=\"UTF-8\"?>
<Package xmlns=\"http://soap.sforce.com/2006/04/metadata\">
    <types>" > package.xml

# Loop through fullNames and insert them into package.xml
for fullName in $fullNames; do
    echo "        <members>$fullName</members>" >> package.xml
done

# Append the rest of the package.xml
echo "        <name>CustomObjectTranslation</name>
    </types>
    <types>
        <members>*</members>
        <name>CustomField</name>
    </types>
    <version>60.0</version>
</Package>" >> package.xml
```

### Delete Metadata

This is not working as expected!!!

Package.xml
```XML
<?xml version="1.0" encoding="UTF-8"?>
<Package xmlns="http://soap.sforce.com/2006/04/metadata">
    <version>60.0</version>
</Package>
```

DestructiveChanges.xml
```XML 
<?xml version="1.0" encoding="UTF-8"?>
<Package xmlns="http://soap.sforce.com/2006/04/metadata">
    <types>
        <members>PaymentMethod</members> <!-- Custom Label Name -->
        <name>CustomLabel</name> <!-- Metadata Type for Custom Labels -->
    </types>
    <types>
        <members>de</members>
        <name>Translations</name>
    </types>
    <version>60.0</version>
</Package>
```
```bash
sf project deploy start --manifest package.xml --pre-destructive-changes destructiveChanges.xml
```
