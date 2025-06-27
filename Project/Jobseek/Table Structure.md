## Field structure
Untuk tiap fieldnya, akan ada struktur seperti ini:
```json
{
	field_name: {
		type: "type",
		order: 1,
		deletable: false,
		options: ["Option 1", "Option 2"]
	} 
}
```

Penjelasan attribute:
#### **`type`**
This attribute will dictates the data type of the field. The possible value of `type` is: 
- `shortText`
- `longText`
- `date`
- `dateTime`
- `enum`
- `link`
- `checkBox`
#### **`order`**
This attributes will dictate what rows will this field will be shown in the table. A newly made field will have the value of `order` as the biggest out of all of the other field (will be shown at the right-most column of the table).

For example, a field has the `order` value of 2. This field will be shown in the 2nd column from the left-most column of the table.

|     | field |
| --- | ----- |
|     |       |
#### **`deletable`**
This attributes will dictate if the field could be deleted or not. This field only set to `false` for a specific column of the table. 

The other column that is made by the user will be set as `true` and cannot be set to `false`.
#### **`options`**
This attribute will dictate what value could the user choose. This attribute only be set to nil for `type` other than `enum`.
### users
```json
{
	_id: "id1",
	firstName: "",
	lastName: "",
	email: "rizkim0071@gmail.com",
	password: "pass1234",
	jobs: ["JOBID1", "JOBID2"],
	structure: {
		jobs: {
			title: {
				type: "shortText",
				order: 1,
				deletable: false,
				options: nil
			},
			description: {
				type: "longText",
				order: 2,
				deletable: false,
				options: nil
			},
			status: {
				type: "enum",
				order: 3,
				deletable: false,
				options: ["Applied", "Rejected"]
			},
			applied_date: {
				type: "date",
				order: 4,
				deletable: false,
				options: nil
			},
			announcement_date : {
				type: "date",
				order: 5,
				deletable: true,
				options: nil
			}
		},
		company: {
			name: {
				type: "shortText",
				order: 1,
				deletable: false,
				options: nil
			},
			description: {
				type: "longText",
				order: 2,
				deletable: false,
				options: nil
			}
		}
	}
}
```
### jobs
```json
{
	id: "jobs1",
	userEmail: "rizkim0071@gmail.com",
	company: "id_company1",
	description: "",
	status: "Applied",
	applied_date: 2025-01-21,
	anouncement_date: 2022-02-23
}
```
### company
```json
{
	id: "company1",
	user_email: "rizkim0071@gmail.com",
	jobs_id: ["jobs1"],
	company_name: "Company 1",
	description: "Company 1 Description",
	
}
```
