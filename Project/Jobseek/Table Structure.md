### users
```json
{
	email: "user1",
	password: "",
	jobs: ["JOBID1", "JOBID2"]
	structure: {
		jobs: {
			title: {
				type: "shortText",
				order: 1
				field: "wajib"
				
			},
			description: "",
			status: ["Applied", "Rejected"],
			announcement_date 
		},
		company: {
		}
	}
},
{
	email: "user2",
	password: "",
	jobs: ["JOBID1", "JOBID2"]
	structure: {
		jobs: {
			title: {
				type: "shortText",
				field: "wajib"
				
			},
			description: "",
			status: ["Applied", "Rejected"]
		},
		company: {
		}
	}
}
```
### jobs
```json
{
	id: "",
	userEmail: "",
	status: nil
}
```

### company
