# SendBatchEmails

The `SendBatchEmails` Apex class is designed to send batch emails to a list of recipients with customizable options, including sender email, sender type, CC/BCC, and the option to send as plain text or rich text (HTML). It also optionally logs the email as an activity against the appropriate records.

## Features

- **Send Emails to Multiple Recipients:** Supports sending emails to a list of recipients or a collection of SObject records.
- **Customizable Sender Options:** Allows specifying a custom sender email address and sender type (Current User, Default Workflow User, Org-Wide Email Address).
- **Rich Text or Plain Text:** Choose whether to send the email as plain text or rich text (HTML).
- **CC and BCC Support:** Supports adding CC and BCC recipients.
- **Log Email Activity:** Optionally logs the email as an activity against related records, such as Cases.

## Usage

This class is designed to be used with Salesforce Flow. You can invoke the `SendBatchEmails` method from Flow by passing the necessary parameters through the `EmailDetails` class.

### Parameters

- **To Addresses List (`toAddresses`)**: List of recipient email addresses.
- **To Addresses Collection (`toAddressesCollection`)**: List of SObject records (e.g., Contacts, Cases, Campaign Members) whose emails will be sent to.
- **Email Subject (`subject`)**: The subject line of the email.
- **Email Body (`body`)**: The body content of the email.
- **Send as Rich Text (`isRichText`)**: Boolean flag to determine if the email is sent as Rich Text (HTML). If false or empty, sends as plain text.
- **CC Addresses List (`ccAddresses`)**: List of email addresses to send a carbon copy (CC).
- **BCC Addresses List (`bccAddresses`)**: List of email addresses to send a blind carbon copy (BCC).
- **Sender Email Address (`senderEmailAddress`)**: Custom sender email address. Leave empty for default.
- **Sender Type (`senderType`)**: Type of sender email. Options include CurrentUser, DefaultWorkflowUser, OrgWideEmailAddress.
- **Log Email Against Record (`logEmailAgainstRecord`)**: Boolean flag to log the email as an activity against the appropriate record (e.g., Contact, Case, Campaign Member).

## Limitations

### Salesforce Flow Builder Limitations

1. **Fixed SObject Type in Flow:**
   - Once a Flow has been created and linked to an `@InvocableMethod` that uses a parameter of type `List<SObject>`, the specific SObject type that Flow expects is set and cannot be dynamically changed within the Flow.
   - This means that if the Flow is configured to work with a specific SObject type (e.g., `Contact`), it cannot easily switch to handling another type (e.g., `Case`) within the same Flow instance.

2. **Manual SObject Selection:**
   - Users must correctly configure the Flow to handle the appropriate SObject type from the outset. If a different SObject type needs to be handled, a separate Flow must be created or the existing Flow must be updated.

### Workarounds

1. **Multiple Flows:** Create separate Flows for each SObject type you need to handle (e.g., one Flow for `Contacts`, another for `Cases`). This ensures that each Flow is configured with the correct SObject type.

2. **Explicit Instructions:** Provide clear instructions to users setting up the Flow, emphasizing the need to configure the correct SObject type and the inability to change it once set.

3. **Error Handling in Apex:** The `SendBatchEmails` class includes error handling to notify users if no valid email addresses are found in the provided lists or collections.

## Installation

1. **Deploy the Apex Class:**
   - Deploy the `SendBatchEmails` Apex class to your Salesforce environment.
   
2. **Create Flows:**
   - Create Flows in Salesforce that invoke the `SendBatchEmails` method, passing the necessary parameters through the Flow's UI.

3. **Configure Email Options:**
   - Ensure that the correct SObject type is selected for the "To Addresses Collection" input parameter when setting up the Flow.

## Example

Here is an example of how to set up the Flow:

1. **Create a Flow:**
   - Go to Salesforce Flow Builder and create a new Flow.

2. **Add an Action:**
   - Add an Action element to the Flow and select the `SendBatchEmails` action.
   
3. **Configure Input Parameters:**
   - Configure the `EmailDetails` input parameters as required.
   - Ensure that the correct SObject type is selected for the "To Addresses Collection" input parameter.

## Contributing

If you find any issues or have suggestions for improvements, feel free to open an issue or submit a pull request on GitHub.
