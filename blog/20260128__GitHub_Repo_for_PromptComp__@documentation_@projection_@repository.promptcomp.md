I plan to make a github repo for this. 

The repo will contain some short introductions like the ones in these documents. That part of the repo is static. Then there will be a folder where various "PromptComp" (PC) compositions will be added. No projections, just the prompts. Maybe add an ancillary file for each projection that projects it into an overview. Then there will be another "contrib" folder where pull requests can put contributions from other users. Eventually we could build up a tree structure of PC files in different categories or topics--but I think a tree is a mistake. A better representation would be a flat list of PC files with descriptive names and #tags in the name to allow category search at the filesystem level.

I think the structure makes sense. It may be easiest to name PC files in the repo starting with a date code (YYYYMMDD) so I can reuse the same title later on in a more refined inquiry. 
Also several of my PC files mention inclusion of specific other PC files rather than repeating them inline. 
I don't want to overcomplicate this, but it seems like a schema or appendix that explains how you can link or nest PC files to build a meta-PC composition. 
Also many of my PC files discuss various technical aspects of contemporary LLMs. So the framework of the repo is model agnostic, but the samples are not.

So for example, in the PC file "INCLUDE PC: 20260121__Vibe-Prose_Seed-Crystal_prompt-evolution-trust-self__@latent-frequency_@individuation_@prompt-as-artifact.promptcomp.md" would (when viewed from the github repo) render to a hyperlink to https://github.com/shsmith/promptcomp/blog/20260121__Vibe-Prose_Seed-Crystal_prompt-evolution-trust-self__@latent-frequency_@individuation_@prompt-as-artifact.promptcomp.md

While I was composing conversations with insertions, the insertion didn't happen right away, but only after a topic needed clarification from a specific insertion. 
I often use the form "consider this previous conversation where we discussed topic X in detail:" + paste the other PC file.

Feels like we are overcomplicating. 
I have had success using this form: "Consider the contents of XYZ.PC" and then after the end of the composition I add a section for each of the named inclusions. 
It creates duplication but keeps a PC file self-contained. 
We can turn this into a more complicated knowledge state engineering in a different/later phase of the project. 
For now maybe just not mention it or do it in examples without explanation since it is usually obvious from context.

I think you understand the Prompt Composition concept. 
Please project that into a README and related documents for a new https://github.com/shsmith/promptcomp repo. 
There will be a few background pages that explain what PromptComp is all about, but the main body of the repo will be a blog folder where I add new compositions from day to day.

These drafts will need some editing but should make it easy for me to wrap up. 

Here are the files I plan to include in the initial commit: 
promptcomp:
  LICENSE    
  README.md  

promptcomp/blog:
  <to be determined>
  20260121__Vibe-Prose_Seed-Crystal_prompt-evolution-trust-self__@latent-frequency_@individuation_@prompt-as-artifact.promptcomp.md
  20260128__GitHub_Repo_Documentation_for_PromptComp__@documentation_@projection_@repository.promptcomp.md

promptcomp/contrib:
  CONTRIB_README.md

promptcomp/docs:
  PromptComp-Philosophy-CRYSTALLIZE-Workflow.md  
  creating-a-promptcomp.md                       
  replaying-a-promptcomp.md                      
  what-is-promptcomp.md

promptcomp/prompts:
  all-in-one-prompt.md               
  attractor-prompt.md                
  request-DAG-prompt.md              
  request-filename-prompt.md         
  request-inputs-verbatim-prompt.md

What is a good "Description" for the promptcomp github repo? (350 chars max) Consider this: Prompt Composition: A new form of writing for the LLM era. PromptComp treats sequences of human prompts as first-class artifacts--executable prose that encodes knowledge states and can be replayed, shared, and projected into multiple formats. Your prompts are the creative work; everything else is projection or performance.

What is a good license type for this? I think MIT would work well. 
Then again, the MIT license refers specifically to "software". Is prompt composition a kind of software? (no)
It is more like a work of art (a script or sheet music--not the performance).

I'm going with this: 
"This work is licensed under CC BY 4.0. You may use, adapt, and build upon this material for any purpose, even commercially, as long as you give appropriate credit."

Help me write a posting to announce the repo.

Thank you for helping me explore these ideas. Please give back verbatim all of my original inputs (my prompts only) from this entire conversation, in chronological order. Do not include your responses, commentary, or formatting--just my exact prompts as I wrote them.
