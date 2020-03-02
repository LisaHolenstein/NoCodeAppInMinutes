# From spreadsheet to no-code app in minutes

Convert an existing expense report process from spreadsheets to a bespoke application in ServiceNow. You'll leave this lab all without writing a single piece of code!

Currently, expense items are put in a spreadsheet and emailed to accounts payable. This process is full of potential issues with data entry, lack of visibility, and inconsistent data entry by employees.

As the process owner, you need to improve the process. Your primary goals are to create a great user experience and improve data consistency for accurate future reports.

In this workshop you will improve the process by creating an application to manage expense reports and line items. You will also import legacy expense spreadsheets into your new app.

*Note: The example application used in this workshop may not be applicable in your organization. However the concepts learned in these lab exercises are applicable to any application.*

## Load the ServiceNow Agent application

1. Use your mobile device to go to the [Apple Store](itms-apps://?action=discover&referrer=app-store) or [Google Play](https://play.google.com/store/apps).

1. Download and install the **ServiceNow Agent** application. Use the following QR Codes from your mobile device for fast access.

    * Google Play Store

        ![Google Play Store](Images/147_NCAIM.png)

    * Apple App Store

        ![Apple App Store](Images/148_NCAIM.png)

    You should see a screen like the following for the ServiceNow Agent app.

    ![Install Agent app](Images/149_NCAIM.png)

1. If prompted for access to location, camera, or sending notifications, click **Allow**.

    > Note: Do not log in to your instance yet. You will do that later when we test your mobile app.

## Getting Started

### Goal

The goal of this lab exercise is to get familiar with the tools available to define the general information needed for your new app.

1. Begin by logging in to your ServiceNow instance with your credentials.
1. Use the left navigation panel to navigate to **System Applications \> Studio**. You can find it easily by typing "Studio" in the filter at the top of the left menu.

    ![Studio](Images/001_NCAIM.png)

1. A new browser tab appears. This is Studio, our integrated development environment (or IDE). This is simply a tool to help manage all the parts of your application. When the popup appears asking if you want to create or import, select **Create Application**.

    ![Create](Images/002_NCAIM.png)

1. From the welcome screen, click **Let's get started**.

   ![Welcome](Images/003_NCAIM.png)

1. The wizard on the screen walks you through the process of building your application. Begin by filling out the name and description.

    | Field | Value |
    | --- | --- |
    | Name | Expense |
    |Description | Manage our expense reports |
    | Scope | (leave unchanged) |

1. If you choose, add an icon for your application. This is optional and does not affect your overall application.

    ![Image](Images/004_NCAIM.png)

1. Click **Create**.
1. On the next screen (_Let's create some roles for this app_), click the **Create** new role link.

    ![Roles](Images/005_NCAIM.png)

1. Under **New role name**, enter "user" and click **Create**.

    ![Role](Images/006_NCAIM.png)  

    > Note the role name is appended to the application scope name. The full name of the role should be something like x_snc_expense.user.

1. Create additional roles for "approver" and "admin".

    ![Roles](Images/007_NCAIM.png)

1. Click **Continue**.
1. From the screen _Which formats do you want to use for this app?_, click **Workspace**, **Mobile** and **Classic**.

    ![Format](Images/008_NCAIM.png)

1. Click **Continue**.

## Defining the Data

### Goal

The goal of this lab exercise is to create the basic data structure for expense reports and line items. The first exercise is to create an expense report table, then a second table for line items based on the legacy spreadsheet. Additionally, you will add some basic access control to the roles defined earlier.

### Create the Expense Report Table

1. From the screen _Which data tables do you want to use for this app?_, click **Create new table**.

    ![Create](Images/009_NCAIM.png)

1. On the next screen, choose **Extend a table**. In the dropdown list below that option, select **Task**. Note, you can start typing "Task" to avoid lengthy scrolling.

    ![Table](Images/010_NCAIM.png)

1. Click **Continue**.
1. From the screen labeled _Great! Let's get going on defining your new table_, click **Continue**.

    ![Table](Images/011_NCAIM.png)

1. On the next screen, in the _Table label_ field, enter **Expense report**.
1. In the _Table name_ change the default name (_x_snc_expense_expense_report_) to **x_snc_expense_report**. After all, who needs the word expense in the table name twice? We can fix that, so why not?!
1. Check the _Auto number_ field and a few additional fields appear. Leave the values as their defaults, they're fine.

    ![Number](Images/012_NCAIM.png)

1. Click the **Manage access** link near the bottom left.
1. To ensure data integrity, we defined a role for each persona earlier. Now it's time to define what each role can do. Remove **Delete permission** from the _user_ and _approver_ roles. Typically, only an _admin_ should delete records and even then it should be under extreme circumstances.
1. Next, remove **Create permission** from the _approver_ role. They shouldn't be creating new expense items.
Your access should now look like the following image:

    ![Access](Images/013_NCAIM.png)

1. Click **Continue**. Your screen should now show success for the Expense report table. Congratulations. Go ahead and click **Continue** again.

    ![Success](Images/014_NCAIM.png)

### Import the Expense Items from Spreadsheet

1. Once again, click **Create new table**.

    ![Table](Images/015_NCAIM.png)

1. This time, choose **Upload spreadsheet**, then click **Continue**.

    ![Table](Images/016_NCAIM.png)

1. Download the sample file: [Expense_Report-Abel_Tuter.xlsx](expense_report-abel_tuter.xlsx).
1. Drag your copy of the downloaded file to the dialog window or click the link and browser to upload it to ServiceNow.

    ![Table](Images/017_NCAIM.png)

1. After uploading the file, check the **Import spreadsheet data** checkbox.

    ![Table](Images/018_NCAIM.png)

1. Click **Continue**.  

    > ServiceNow will take a moment to process your spreadsheet. It determines what fields to create based on the column headings in your spreadsheet. It also stages the spreadsheet rows before placing them in the resulting ServiceNow table. When complete, it displays the screen below.

    ![Table](Images/019_NCAIM.png)

1. Before modifying any existing fields, click **Add a new field** to connect the new table with spreadsheet information to the existing _Expense report_ table.
1. Fill in the fields from the following table:

    | Name | Value |
    | --- | --- |
    | Field Label | Expense report |
    | Field name | expense_report |
    | Field type | Reference |
    | Reference table | Expense report [x_snc_expense_report] |

    ![Table](Images/020_NCAIM.png)

1. At this point you get to address the issue of data consistency and give an improved experience in ServiceNow. The Now Platform offers more field types than Excel does so it makes sense to take advantage of them. For example, rather than having someone enter their name, they can pick it from a predetermined list. Begin by locating the **Receipt status** row and clicking the **down arrow** next to String.

1. From the dropdown list, choose **Choice**.

    ![Table](Images/021_NCAIM.png)

1. After choosing _Choice_, note that the right column changes to _Choice type_. Choose the option **Dropdown without none**.

    ![Table](Images/022_NCAIM.png)

1. Click the **down arrow** next to the choice type to reveal the _choice options_.

    ![Table](Images/023_NCAIM.png)

1. Click the link **+ Add a new choice**.

    ![Table](Images/024_NCAIM.png)

1. Add the _Display value_ of **Yes** and _System value_ of **yes**.

    ![Table](Images/025_NCAIM.png)

1. Repeat the process of adding a new choice to add a _Display value_ of **No** and _System value_ of **no**.

    ![Table](Images/026_NCAIM.png)

1. Using the same method, change the field type of _Expense type_ from String to **Choice**, and **Dropdown with none**.
1. In the choice options, check the box **Mandatory**.
1. Add the choices in the following table:

    | Display value |System value |
    | --- | --- |
    | Transportation | transportation |
    | Dining | dining |
    | Hotel | hotel |

    ![Table](Images/027_NCAIM.png)

1. Finally, change the _Employee_ field type to **Reference**.
1. Set the _Reference table_ to **User \[sys_user\]**.

    ![Table](Images/028_NCAIM.png)

1. Click **Continue**.
1. On the following screen, fill in the _Table label_ as **Item**. (The table name will auto-populate. Leave it as is.)

    ![Table](Images/029_NCAIM.png)

1. Click the **Manage access** option at the bottom of the form. Note, you may have to scroll to see all the options. This is where we set "who has what access" to your records.
1. To ensure data integrity, we defined a role for each persona earlier. Now it's time to define what each role can do. Remove **Delete permission** from the _user_ and _approver_ roles. Typically, only an _admin_ should delete records and even then it should be under extreme circumstances.
1. Next, remove **Create permission** from the _approver_ role. They shouldn't be creating new expense items.  
   Your access should now look like the following image:

    ![Table](Images/030_NCAIM.png)

1. Click **Continue**. If everything worked, you should have a screen like this:

    ![Table](Images/031_NCAIM.png)

1. Click **Continue**.
1. At this point ensure both the _Expense report_ and _Item_ tables are selected and click **Done with tables**.

    ![Table](Images/032_NCAIM.png)

## Designing Your App

### Goal

The goal of this lab exercise is to define the user experience your app presents. In the earlier lab, you chose Workspace and Classic. This section completes the details needed to access your app through either of these interfaces.

### Configuring Workspace

1. On the _Workspace_ row, click **Start**.

    ![Workspace](Images/033_NCAIM.png)

1. This screen really doesn't need any configuration. You can optionally put in a description if you like.

    ![Workspace](Images/034_NCAIM.png)

1. Click **Continue**.
1. The Workspace UI provides two options for navigating records. _Tabbed navigation_ and _Single page navigation_. Each has their strengths based on the use case. For our expense report app, click **Tabbed navigation** then click **Continue**.

    ![Workspace](Images/035_NCAIM.png)

1. In the following window, click **Continue**.

    ![Workspace](Images/036_NCAIM.png)

1. In the following window, click **Continue**.

    ![Workspace](Images/037_NCAIM.png)

1. Validate your workspace configuration by clicking **Open**.

    ![Workspace](Images/038_NCAIM.png)

    > IMPORTANT: Note the URL **`https://[yourinstance].service-now.com/now/workspace/expense/home`**

### Configuring Mobile

1. Return to the Studio browser tab.
1. Click **Start** (shown below) to configure the Mobile UI.

    ![Mobile](Images/039_NCAIM.png "Mobile")
    ![Mobile](Images/040_NCAIM.png "Mobile")

1. Make sure that _snc_expense_admin_ role is selected here as well.
1. Leave the rest this as is and click on **Create**.

### Configuring Classic UI

1. Return to the Studio browser tab.
1. Click **Start** (shown below) to configure the Classic UI.

    ![Classic](Images/042_NCAIM.png "Classic")

1. In the following screen, click **Create**.

    ![Classic](Images/043_NCAIM.png "Classic")

1. Click **Done with apps**.

    ![Classic](Images/044_NCAIM.png "Classic")

1. Click **Done**.

    ![Classic](Images/045_NCAIM.png "Classic")

## Test your mobile app

1. On your mobile device, open the ServiceNow Agent app you downloaded earlier.

1. Provide the URL and a nickname for your instance.

    ![Mobile](Images/150_NCAIM.png)

1. Tap **Save and Login**

1. Provide your admin userid and password used to login to your instance earlier and tap **Login**.

    ![Mobile](Images/151_NCAIM.png)

1. Tap **Allow** to enable access from your mobile device to your instance.

    ![Mobile](Images/152_NCAIM.png)

1. At the bottom of the screen, tap the **Expense** navigation tab.

1. Tap **Expense report** to display the list of expense reports.

    ![Mobile](Images/154_NCAIM.png)

1. Tap around to see if your list of expense items is also available.

    >Q: What do you notice about the list of expense reports and items? A: The expense report and items are not "related" to each other yet. Yes, there's more we can do here, but in the interest of time we're going to stick with the desktop UI for now. Let the instructor know if you're interested in learning more about mobile development.

## Designing Your Form

### Goal

The goal of this lab exercise is to build the form for your application. You will add the details of the form and list layout to the item and expense report tables in the classic interface.

### Expense Report form Layout

1. In Studio, use the Application Explorer on the left to navigate to **Data Model\> Tables\> Expense Report**.

    ![Form](Images/046_NCAIM.png "Form")

1. In the form that appears, scroll down to the Related Links section and click **Design Form**.

    ![Form](Images/047_NCAIM.png "Form")

1. The Form Designer window appears with the current default layout for the Expense Report form. Using the "X" on the right hand side of the field, remove the following fields from the form layout:

    * Priority
    * Parent
    * Configuration item

    ![Form](Images/048_NCAIM.png "Form")

1. On the left, use the list of fields to select the following fields and drag them on to the form designer.

    * Opened by
    * Activities (filtered)

    ![Form](Images/049_NCAIM.png "Form")

1. Click the **gear icon** next to _State_ to configure the choices as follows:

    | Label | Value |
    | --- | --- |
    | Pending | (deleted) |
    | Draft | 1 |
    | Approval | 2 |
    | Approved | 3 |
    | Rejected | 4 |
    | Canceled | 7 |

    ![Form](Images/050_NCAIM.png "Form")

1. Click the **X** in the upper right of the _Properties_ popup window to close it.
1. Organize the other fields on the form to make the form appear similar to the following:

    ![Form](Images/051_NCAIM.png "Form")

1. Next, click the **Save** button in the upper right of the form.

1. Now that the default view is defined, replicate the form layout to workspace. Begin by clicking the dropdown next to Default view at the top of the Form Designer and choosing **New**.

    ![Form](Images/052_NCAIM.png "Form")

1. In the popup that appears, enter the view name workspace and click **OK**.

    ![Form](Images/053_NCAIM.png "Form")

1. Save the form design again by clicking **Save** in the upper right.

### Add the related lists for Classic UI and Workspace UI

1. Within Studio, click the **Create Application File** link in the upper left corner.

    ![List](Images/054_NCAIM.png "List")

1. In the window that appears, select **Forms \& UI \> Related List**.

    ![List](Images/055_NCAIM.png "List")

1. Click **Next**.

1. Under _My Tables_, click your _Expense report_ [x_snc_expense_report]. The naming convention for your Report may be different, so just select the report you created.

    ![List](Images/056_NCAIM.png "List")

1. Click **Create**.
1. Select _Item -\> Expense Report_ and the _Approvers_ and ADD both to the selected using the arrow:

    ![List](Images/057_NCAIM.png "List")

    ![List](Images/058_NCAIM.png "List")

1. Click **Save** to save the work on the related list for the _Classic UI_.

1. At the bottom of the form, locate the _View name_ field and select **New**.

    ![List](Images/059_NCAIM.png "List")

1. In the _Create New View_ window that appears, type in the _View name_ workspace and click **OK**.

    ![List](Images/060_NCAIM.png "List")

1. Scroll down the Available list on the left and select the **Item -\> Expense** report entry.

    ![List](Images/061_NCAIM.png "List")

1. Use the \> icon to move the entry from the left to right.
1. Press the **Save** button
1. Next you will create a related list in the Workspace view.
1. Do the same for Approvers Related list

    ![List](Images/062_NCAIM.png "List")

1. Click **Save**.
1. Validate your work by going to your Workspace browser tab.
1. Click the **Lists icon** (☰) on the left.
1. Navigate to **Expense reports \> All** and click **New**.

    > Note:
    > If a blue display message appears, use the "X" to close it in order to display the Save button.
1. Click **Save**.
1. You should now see the _Items_ list as shown in the image below.

    ![List](Images/063_NCAIM.png "List")

## Create your workflow

### Goal

The goal of this lab exercise is to create a simple workflow on your application. You will add create the trigger for the workflow, include the approval subflow, add a few actions, and test the workflow.

1. In Studio Create New Application File, Flow and click **Create**.

    ![Flow](Images/064_NCAIM.png)

1. Select **Flow** and click **Next**

    ![Flow](Images/065_NCAIM.png)

1. Change the Flow properties and add the Name: **Approval**.

    ![Flow](Images/066_NCAIM.png)

1. Click on **Submit** to save the changes.

    ![Flow](Images/067_NCAIM.png)

### Set the trigger

1. Click on the **(+)** sign to open the options for setting the trigger
1. Select **Created or Updated**

    ![Flow](Images/068_NCAIM.png)

1. Select the _Expense report_ Table

    ![Flow](Images/069_NCAIM.png)

1. Add the _Condition_ you want to use for this trigger by clicking on the **(+)** sign _Add filter_: **State \> changes to \> Approval**

    ![Flow](Images/070_NCAIM.png)

1. Select **For each unique change**, as we want this to occur anytime this record changes and confirm with **Done**.

    ![Flow](Images/071_NCAIM.png)

### Include subflow and create actions

The approval subflow should already exist in your lab instance. If you're doing this lab in a **Personal Developer Instance (PDI)**, you'll have to either import the update set or create the subflow yourself. You'll find the instructions further down in the _Challenge exercise_ part of this lab guide.

1. Click the **(+)** sign to add a _Subflow_.
1. Choose **2 step group approval**.

    ![Flow](Images/072_NCAIM.png)

1. Drag the **Data pill** "Expense Report Record" to the "Task" field in the Subflow.

    ![Flow](Images/073_NCAIM.png)
    ![Flow](Images/074_NCAIM.png)

1. Confirm with **Done**.
1. Click the **(+)** sign to add _Flow Logic_.
1. Choose **If**.
1. Set **Condition:** to _Approved_.
1. Drag the **Data pill** "1 - 2 step group approval \> Approval Status" to **Condition 1:**.

    ![Flow](Images/075_NCAIM.png)

1. Set **Approval Status \> is \> Approved**.

    ![Flow](Images/076_NCAIM.png)

1. Confirm with **Done**.
1. Below the _if branch_, click the small **(+)** sign to add _Flow Logic_.

    ![Flow](Images/077_NCAIM.png)

1. Click on **Action**, filter for "Update", and choose **Update Record**

    ![Flow](Images/078_NCAIM.png)

1. Drag the **Data pill** "Expense Report Record" to the "Record" field in the Action.
1. Click **+ Add Field Value**.
1. Select a field: **State**.
1. Select a choice: **Approved**.
1. Confirm with **Done**.

    ![Flow](Images/079_NCAIM.png)

1. In the main thread of the flow, click the **(+)** sign to add _Flow Logic_.

    ![Flow](Images/080_NCAIM.png)

1. Choose **Else If**.
1. Set **Condition:** to "Rejected".
1. Drag the **Data pill** "1 - 2 step group approval \> Approval Status" to **Condition 1:**.
1. Set **Approval Status \> is \> Rejected**.
1. Confirm with **Done**.

    ![Flow](Images/081_NCAIM.png)

1. Repeat the above steps with the option "Rejected":
1. Below the else if branch, click the small **(+)** sign to add _Flow Logic_.
1. Click on **Action**, filter for "Update", and choose **Update Record**
1. Drag the **Data pill** "Expense Report Record" to the "Record" field in the Action.
1. Click **+ Add Field Value**.
1. Select a field: **State**.
1. Select a choice: **Rejected**.
1. Confirm with **Done**.
1. **Save** the flow.
1. The complete flow should look like this:

    ![Flow](Images/082_NCAIM.png)

### Testing the created workflow

1. Click on the Test button to test your workflow:

    ![Flow](Images/086_NCAIM.png)

1. Click on the **(+)** sign to create a new record so you can Test the flow.

    ![Flow](Images/087_NCAIM.png)

1. This opens the Request form for the Expense report. Add a _Short Description_, make sure to change _Opened by_ to **David Loo** and click **Submit**.

    ![Flow](Images/088_NCAIM.png)

1. Click **Run Test** and wait for the Flow to be executed. The message “Flow has been executed. To view the flow, click here.”. Click on the **Green link**.

    ![Flow](Images/089_NCAIM.png)

1. Below you will see all the details for the Flow.

    > Note:  
    > The state is waiting, due to the requested approval

1. Click **Open Current Record** and **Open Record** to go to the Expense record.

    ![Flow](Images/090_NCAIM.png)

1. Go to the _Approvers_ related list **right click** on _Requested_ and select **Approve**.

    ![Flow](Images/091_NCAIM.png)

    > Note:  
    > The approval was sent to the manager of David Loo, by the flow we created. Because we are logged in as administrator we can overwrite the approval. Normally this can be done via email or mobile app.

1. Reload the form (or _Approvers_ related list) to see that the second approval step, the group approval has been created. Check out the flow window, open the subflow with the grey triangle to see the update.

    ![Flow](Images/083_NCAIM.png)

1. **Right click** again on _Requested_ in Beth Anglin's row and **Approve** the record.

    ![Flow](Images/084_NCAIM.png)

1. The ticket state should now change to approved, and this change is shown in the activities. If not reload the page

    ![Flow](Images/092_NCAIM.png)

1. Refresh the flow history, review it and make sure you understand the steps.
1. Click **Activate** and _Confirm Flow Activate_ to publish the Flow. Now it will run, whenever an Expense Report's status changes to _Approval_.

## Finishing Touches

### Goal

The goal of this lab exercise is to put the finishing touches on your application. You will add the details of the form and list layout to the item table in workspace interface.

### Configure Item Form Layout

1. From _Studio_, open the **Item table** record.
1. Click the **Design Form** link.
1. Arrange the fields similar to the image below and click **Save**.

    ![Form](Images/098_NCAIM.png)

1. Create a new view called **workspace** the same way you did for the _Expense report_ form design.
    1. Use the dropdown next to _Default view_
    1. Click **New**.
    1. Enter the view name **workspace**.
    1. Click **OK**.
    1. Click **Save**.

1. Validate your work in _Workspace_ by going to **Lists \> Items \> All** and open a record. Your form should appear similar to the following:

    ![Form](Images/099_NCAIM.png)

### Configure the Items List Layout in Workspace

1. Next, let's clean up the default list layout for the items in _Workspace_. Begin by going to the _classic UI_ and navigating to **Workspace Experience -\> Agent Workspace Guided Setup -\> Lists -\> Create filtered lists**.
1. Click **Get Started**.

    ![Workspace](Images/155_NCAIM.png)

    ![Workspace](Images/100_NCAIM.png)

1. Click **Configure** under _Create filtered lists_.

    ![Workspace](Images/085_NCAIM.png)

1. Using the list filter, locate the records with **Category Items**.

    ![Workspace](Images/101_NCAIM.png)

1. Click the **Run** button.
1. Open the record with the list name **All**.

    ![Workspace](Images/102_NCAIM.png)

1. Click the **lock** next to the _Columns_ field.
1. Arrange the items in the _Selected_ column using the left/right and up/down arrows to reflect the list below:
    * Transaction date
    * Account
    * Amount
    * Business purpose
    * Employee
    * Expense report
    * Expense type
    * Receipt status
    * Vendor name

    Your columns should now look like this:

    ![Workspace](Images/103_NCAIM.png)

1. Click **Update**.
1. Validate your work by going to workspace and refreshing your browser window.

    > Note, do not use the list refresh icon. You should see your new list layout take effect.

    ![Workspace](Images/104_NCAIM.png)

## Challenge exercises

### Configure the Classic UI Expense Report List Layout

1. In the classic UI, navigate to **Expense \> Expense report \> Open**.
1. From the list, click any column heading menu (☰) and choose **Configure \> List Layout**.

    ![List](Images/107_NCAIM.png)

1. Using the same method as earlier, select the following columns on the right.
    * Number
    * Opened by
    * State
    * Assigned to
    * Short description

    ![List](Images/108_NCAIM.png)

1. Click **Save**.
1. Verify your work by inspecting the list layout as shown below:

    ![List](Images/109_NCAIM.png)

### Associate the Existing Items to an Expense Report

1. In the classic UI, update the _Opened by field_ from the _Expense report list view_ by **double-clicking** on the table cell of the record (being careful not to click the link).

    ![List](Images/110_NCAIM.png)

1. Type the name **Abel Tuter** and click the green checkmark.
    > Note:  
    Abel Tuter matches the name on the expense item records imported earlier.  
    > **IMPORTANT**: Make note of the expense report record number you updated!

    ![List](Images/111_NCAIM.png)

1. Navigate to **Expense \> Item \> All**.

    ![List](Images/112_NCAIM.png)

1. Hold down the **shift-key** and **drag your cursor** to select the records where the Expense report column displays _(empty)_.

    ![List](Images/113_NCAIM.png)

1. **Double-click** next to the word _(empty)_ to edit multiple cells.

    ![List](Images/114_NCAIM.png)

1. Enter the expense report number or use the magnifying glass (![List](Images/115_NCAIM.png)) to locate the record and click the green checkmark to save your results.

    ![List](Images/116_NCAIM.png)

1. Validate your work by navigating to **Expense \> Expense report \> Open**.
1. Open the record you just added the items to.

    ![List](Images/117_NCAIM.png)

1. Verify your screen looks similar to the one below with the line items in the list.

    ![List](Images/118_NCAIM.png)

### Import a second Spreadsheet of Items

1. Download the second Excel spreadsheet [Expense_Report-Luke_Wilson.xlsx](expense_report-luke_wilson.xlsx).

1. In the classic UI, navigate to **Expense \> Item \> All**.

    ![List](Images/119_NCAIM.png)

1. From the list, click any column heading menu (☰) and select **Import**.

    ![List](Images/120_NCAIM.png)

1. On the screen that appears, uncheck _Do you want to create an Excel template to enter data?_.
1. Click **Choose File** and navigate to the location where you saved your downloaded file.

    ![List](Images/121_NCAIM.png)

1. Click **Upload**.
1. When the upload is complete, click **Preview Imported Data**.

    ![List](Images/122_NCAIM.png)

1. Verify there are 4 rows of records imported and no errors or warnings.
1. Click **Complete Import**.

    ![List](Images/123_NCAIM.png)

1. Validate the records were imported to the Items table.
1. Optionally, create a new expense report record for Luke Wilson and associate the new items to the Expense report.
1. Does Luke's expense report show his imported items?

### (OPTIONAL) Create Approval subflow

For the purpose of this lab, we will create a subflow with 2 approval steps. The first is a simple manager approval, the approval will be assigned to the manager of the person that created the Expense report (Opened by). Once the manager has approved, a second approval will be assigned to a group. Every member of the group will receive an approval record. As soon as one member of the group approves, the result will be assigned to the subflow output. If the manager has not approved, this result will then be assigned to the output. This output can be used in the parent flow.

> **What is a subflow?**  
> A subflow is a sequence of reusable actions that can be started from a flow, subflow, or script. Define inputs and outputs to pass data to and from the subflow.  
> All subflows consist of _properties_, one or more _inputs_, one or more _outputs_, a sequence of _actions_, and the _data_ collected or created. Unlike flows, subflows:
>
> * Do not have a trigger and are instead started from a parent flow, subflow, or script by a method call.  
> * Include inputs to specify data available to the subflow when it starts.  
> * Include outputs to specify data available to the parent flow after the subflow ends.
>
> Using subflows, process analysts can:
>
> * Create a set of reusable operations for use in multiple flows.  
> * Add flow logic in addition to actions.  

1. In Studio, click **File**, choose **Switch**, then click on **Create Application**
1. Name your application "Approval Subflow" with the scope "x_snc_approval_sf" and click **Create**

    ![Subflow](Images/125_NCAIM.png)

1. Choose **Continue in Studio (Advanced)**.

    ![Subflow](Images/126_NCAIM.png)

1. Open your application **"Approval Subflow"**.
1. Within Studio, click the **Create Application File** link in the upper left corner.
1. Filter for "Flow" and click on **Create**.

    ![Subflow](Images/127_NCAIM.png)

1. Choose "SubFlow" and click **Next**.

    ![Subflow](Images/128_NCAIM.png)

1. Name your subflow and optionally add a description. Click **Submit**.

    ![Subflow](Images/129_NCAIM.png)

1. With the plus sign **(+)** on the right of the input section, add an input to your subflow, label it "Task", check that the Name is "task", and from the Type picker choose **Reference \> Task \[task\]**. Make this input **Mandatory**

    ![Subflow](Images/130_NCAIM.png)

1. With the plus sign **(+)** on the right of the output section, add an output to your subflow, label it "Approval Status" and set the Name "approval_status", and from the Type picker choose **Choice**.

    ![Subflow](Images/131_NCAIM.png)

1. Under **Advanced options** change **Create new choice list** to **Reference existing choice list on a table** and set the **Choice table** to **Approval \[sysapproval_approver\]**, set **Choice field** to "State", and **Default value** to "Cancelled". Then click **Done**.

    ![Subflow](Images/132_NCAIM.png)

1. Click the **(+)** sign to add an _Action_ for this subflow.
1. Click on **Action**
1. Select **Ask For Approval** Action

    ![Subflow](Images/133_NCAIM.png)

1. Drag the **Data pill** "Task" from the Subflow Inputs on the right into the field "Record".

    ![Subflow](Images/145_NCAIM.png)

1. Set the **Rules** to "Approve or Reject" When: "Anyone approves or rejects".
1. From the pill picker next to the approval conditions navigate to **Subflow Inputs \> Task \> Opened by \> Manager**.

    ![Subflow](Images/146_NCAIM.png)

1. Confirm with **Done**.
1. (Optional) Add a comment "Manager Approval" to approval step.
1. Click the **(+)** sign to add _Flow Logic_ to this subflow.
1. Choose **If**.

    ![Subflow](Images/134_NCAIM.png)

1. Set **Condition:** to "Manager approves".
1. Drag _Approval State_ from **Step 1- Ask for Approval** to **Condition 1:**. Select **is** and **Approved**.
1. Confirm with **Done**.

    ![Subflow](Images/135_NCAIM.png)

1. Click the **(+)** sign below the **if** to add an _Action_ in this branch.

    ![Subflow](Images/136_NCAIM.png)

1. Click on Action
1. Select **Ask For Approval** Action
1. Drag the **Data pill** "Task" from the Subflow Inputs on the right into the field "Record".
1. Set the **Rules** to "Approve or Reject" When: "Anyone approves or rejects".
1. From the icon with 2 people choose the Assignment Group **Service Desk**.

    ![Subflow](Images/137_NCAIM.png)

    ![Subflow](Images/138_NCAIM.png)

1. Confirm with **Done**.
1. (Optional) Add a comment "Group Approval" to approval step.
1. Below the group approval, click the **(+)** sign to add _Flow Logic_.
1. Choose **Assign Subflow Outputs**.

    ![Subflow](Images/139_NCAIM.png)

1. Click on the **(+)** sign on the right, select output "Approval Status" and from the pill picker, choose **2.1 - Ask for Approval \> Approval State**.

    ![Subflow](Images/140_NCAIM.png)

    ![Subflow](Images/141_NCAIM.png)

1. Confirm with **Done**.
1. (Optional) Set step comment to "Assign group approval state to output" to Assign output step.
1. In the main thread of the flow, click the **(+)** sign to add _Flow Logic_.
1. Choose **Assign Subflow Outputs**.

    ![Subflow](Images/142_NCAIM.png)

1. Click on the **(+)** sign on the right, select output "Approval Status" and from the pill picker, choose **1 - Ask for Approval \> Approval State**.

    ![Subflow](Images/143_NCAIM.png)

1. Confirm with **Done**.
1. (Optional) Set step comment to "Assign manager approval state to output" to Assign output step.
1. (**Save** and) **Publish** the subflow.
1. The complete Subflow should look like this:

    ![Subflow](Images/144_NCAIM.png)
