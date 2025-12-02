
# Field Dependency Filter for Zendesk

Automatically filters Zendesk ticket dropdown field options based on parent field selections.

---

## Features

- Dynamically filters child dropdown options according to the selected parent field value
- Easy configuration of custom filter rules to match your business logic
- Supports complex field dependencies for advanced workflows
- Improves agent efficiency and accuracy
- Reduces clutter and confusion in ticket forms

---

## How It Works

When an agent selects a value in a parent dropdown field, only the relevant options will appear in the dependent child field. This guides agents through the ticket process, ensuring they select valid and context-sensitive options.

---

## Installation

### Prerequisites

- Zendesk Support account with admin access
- [Zendesk CLI](https://developer.zendesk.com/documentation/apps/app-developer-guide/zcli/) installed

### Steps

1. Package the app using the Zendesk CLI:
	 ```sh
	 zcli apps:package
	 ```
2. Upload the generated zip file to your Zendesk instance via the Admin Center.
3. Install the app in your Zendesk account.
4. Configure the filter rules in the app settings according to your field dependencies.
5. Save and reload your ticket interface to activate the filtering.

---

## Configuration

Each rule you add to the app settings describes a single parent→child relationship and accepts these properties:

- `name`: Friendly label shown only inside the app configuration page.
- `parent`: Numeric ID of the parent dropdown field.
- `child`: Numeric ID of the dependent dropdown field that should change based on the parent.
- `mapping`: Dictionary where every key is a parent option tag and the value is an array listing the tags of the child options that should remain visible when that parent option is selected.

Because the mapping uses tags, make sure you read them directly from the option settings (not the displayed labels). Every parent option you want to handle must have an entry, and each entry enumerates all allowed child option tags for that parent value.

Example configuration:

```json
{
	"rules": [
		{
			"name": "Reason → Subreason",
			"parent": "123",
			"child": "456",
			"mapping": {
				"reason1": [
					"subreason1",
					"subreason2",
					"subreason3"
				],
				"reason2": [
					"subreason4",
					"subreason5",
					"subreason6"
				]
			}
		}
	]
}
```

Refer to your Zendesk field IDs and option values when configuring rules.

---

## Data Disclosure & Privacy Notice

Field Dependency Filter accesses and processes the following data within your Zendesk account:

- Ticket field metadata (field IDs, option values)
- Agent selections in ticket forms
- Filter rules configured by administrators

No ticket content, user data, or sensitive information is stored or transmitted outside your Zendesk instance. All processing occurs client-side within the Zendesk interface.

For more information, please review our [Privacy Policy](https://github.com/braamcamp/zendesk-field-dependency-filter/blob/main/PRIVACY.md) or contact support for details about data handling and compliance.

---

## Support

For questions, issues, or feature requests, please open an issue on [GitHub](https://github.com/braamcamp/zendesk-field-dependency-filter/issues) or contact the author at andre.oliveira@zendesk.com.
