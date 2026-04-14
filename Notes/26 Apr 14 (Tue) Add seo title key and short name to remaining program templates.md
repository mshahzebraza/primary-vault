---
type: "[[Task]]"
categories:
  - "[[Personal]]"
  - "[[Work]]"
  - "[[Tasks]]"
date: 2026-04-14
tags:
  - script
  - backfilling
organization:
  - "[[scholarbee]]"
projects:
  - "[[sb-ops-scripts]]"
status:
  - active
priority: P1
---

## Overview
> The [[26-Apr-06 (Mon) Task - Commit the program template data from data entry into the database]] task didn't update all the program templates for some reason, and about 650 entries need to be assigned the short name and seo title manually.

## Pseudo Code
```ts title:"phase-1 generation"

class ProgramTemplatesMissingInfoGenerator(){
	private system_prompt:string;
	
	constructor(system_prompt){
		this.system_prompt=system_prompt
	}
	
	private saveToFileSystem(generated_data, user_prompt){
		// ... save the generated_data in the file_system
	}
	
	private createUserPrompt(input_data){
		// ... handle the input to user prompt creation using a template ...
		
		return user_prompt
	}
	
	private retrieveAiResponse(user_prompt){
		// ... call AI to get the response in json
		
		// .. validate the ai response structure using schema validation
	}
	
	generator(input_data){
		const userPrompt = createUserPrompt(input_data);
		
		const aiResponse = retrieveAiResponse(userPrompt);
		
		// TODO: Should also add the properties like status for review
		// TODO: Should also create a visual editor in html for easier review
		await saveToFileSystem(aiResponse, userPrompt);
		
		return aiResponse;
	}
	
}

// run with <script-file> generate
// main IIFE
(function (){
	const MAX_BATCH_SIZE=50;
	const db = connectToDb('conn-string');
	const prog_templates_col = db.program_templates
	
	// Array({_id, name, degree_level})
	const templatesToBackfill = extractDocsToBackfill(program_templates_col);
	const templatesToBackfillBatches = batchMaker({
		data: templatesToBackfill,
		maxBatchSize: MAX_BATCH_SIZE
	});
	
	// initialize ai connection with system_prompt
	const missinInfoGenerator = new ProgramTemplatesMissingInfoGenerator({
		system_prompt
	})
	
	// Use AI to request the short-name and seo_title_key
	// Array({originalData, userPrompt, returnedData}) 
	// ? returedData: Array({_id, short_name, seo_title_key})
	const dataBatches = templatesToBackfillBatches.map((data, idx)=>{
		// handles the user_prompt generation as well as extraction of data
		// Combine & Save the results into file-system along with the real data
		return missingInfoGenerator.generator(data);
	})

	// TODO: Log out the summary of the generation process
	// Total Documents to Backfil: --
	// Total Generation by AI: --
	// All Review Files Saved at: output/<path-to-dir>
	// Please update the files in place by assigning the status
	// Then run the script with these arguments:
	// <script-file> ingest
	// which by default looks at the reviewed files in the defualt output dir
	
	
})()


```

## Current Tasks
- [ ] 





![[Related Meetings.base]]

## 2026-04-14
