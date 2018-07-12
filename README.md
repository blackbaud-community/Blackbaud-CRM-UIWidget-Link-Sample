# Blackbaud-CRM-UIWidget-Link-Sample

Embedding UIWidgets on your pages is a great way to extract data from CRM and view it at a glance! This code sample shows just a couple ways to can use UIWidgets to not only show information, but also provide a way to link your application users to useful and relevant pages in the system.

## Getting Started

To get started, simply download the code and load the package spec `TopProspects.Package.xml` into your local CRM installation. This will load all of the components in the code sample, plus modify the My Fundraiser Page to show the new widget. To access the My Fundrasier Page, you will need to perform the following steps in CRM:

1. Add yourself as a Constituent.
2. Add the Fundraiser constituency to your Constituent record. This can be done either by accessing the Personal Info > Constituencies tab on your Constituent Page or by going to the Prospects functional area and selecting "Add a fundraiser."
3. Link your app user to your Constituent record. From the Constituent Page, you can do this by selecting "Edit link to user" on the left side under Tasks.

Now, you can go to the Prospects functional area and select "My fundraiser page" under "Prospect management!" The "Prospects and Plans" tab on that page should show the UIWidget.

## Links on the Widget

You will need to have at least one prospect in your database for the widget to return any results. If you do not have a prospect, follow these steps:

1. Add a new Constituent.
2. On the Personal Info > Constituencies tab on that constituent's page, add the Prospect constituency. They should now appear in the widget.

Now that the list is populated, you should notice two links:

* the constituent's name within the list on the widget
* a "more" link on the widget's lower right corner

Let's take a look to see how these are made.

### Name

This link will take you to the Constituent Page for the person whose name you click. It's built by the following code, found in the UIWidget spec.

``` xml
<LinkAction LinkFieldID="NAME">
    <!-- Constituent.Page.xml -->
    <ShowPage PageID="88159265-2B7E-4c7b-82A2-119D01ECD40F" TabID="966a756b-4b38-47bc-8c6a-de82035cb0a7">
    <ActionContext>
        <DataListField>ID</DataListField>
    </ActionContext>
    </ShowPage>
</LinkAction>
```

Note that both the `LinkFieldID` and the `DataListField` come from `OutputField`s specified on the Data List spec. We are transforming the Name field to be a link to the Prospect tab on the Constituent page, and providing the constituent's ID provided by the data list.

### More

This is added simply by using the `MoreLink` feature defined within the XML schema for the UIWidget spec type.

``` xml
  <MoreLink>
    <!-- Prospect.Page.xml -->
    <ShowPage PageID="1a01610e-4937-4d70-b705-d1947efbe3c7" />
  </MoreLink>
```

Currently, this feature supports linking to a page without context, so these links should take the user to an area in the application that displays general information, rather than specific information related to a given record.