For the commit messages part, it looks at the ten recent commits and summarises them, just by looking at the diff itself ? and displays a natural language summary. 
When more things are committed after the latest 10, are the previous ones still stored in the db, and are the new commit summaries to display automatically updated in realtime in this app?
what is the actual use of typescript? define clearly what you mean when you say advantage because it is type safe in simple language and some example, or what would happen otherwise
and to follow up on that, what would be specefic reason why we would prefer tRPC for this instead of other API. how does it differ from REST. give example of what would things like in REST vs tRPC, and then clearly point out why it works out in our case
why are we using tanstack query, and not some other usual thing for client side, specefic use case or replaceable
for the audio files, we are using assembly ai for transcribing them, then storing both the transcript (in postgres?) and audio itself (in firebase?), why are both of them needed, shouldn't we discard the audio after we have the transcript? seems redundant

and now the main and most important question: 
is this how the recursive flow looks like for the onboarding the files : 
we take files one by one, pass them to gemini (LLM), and get a summary, then create an embedding out of the summary (768 dim), and then store the summary, original source file, name of the file, and embeddings as one entry? if chunking takes place where does it happen?
and when we talked about using pgvector for vector db, how does this work (like in our database that we create containing several tables, one of the tables is vector one and they live in the same space, where joins can happen between the vector and non vector ones? or is just one field on the normal table vector, the embeddings one? or they live in seperate spaces), clarify

also once the summaries are made, and the whole object along with embeddings and all is appended to the db, and then at a later point, someone commits code (creates a new file, or mainly modify an already existing file), then do we also update the already existing summary? because maybe it changed what the file does, or how it does it?
and as for the summary, they are only with respect to single files right? not a whole bird eye view of how the files work together? the summary just contains what the single files does?

why do you mention this tool is only appropriate for only short repos? what would be the problem with larger ones?

do answer to the premade questions on the qna page, in case a commit was made later on, and it affected the answer to one of those questions

recheck or correct me on the answer flow: 
user gives a prompt, we make an embedding, search the vector db for the similarity, 
get an entry from db, with summary as well as source code, feed that to gemini, and then it answers

and for the meeting flow: 
we upload the audio, assembly ai gets the transcript, fireflies reads that transcript and divides them into sensible topics and actions, and stores it on the db, (are both the raw transcript, and topics and actions both stored into the db), the audio is also stored on firebase

explain clearly why in our pg vector was sufficient, but for larger repos you would need a proper vector db. explain with some examples, on how they work differently and handle stuff better 

since this is an AI project, we need some sort of evals, so clearly lay out how one would do the evals for the project, simply, step by step. to score the model, on what is the accuracy of the answers, and maybe also trying with different methods to see if they improve accuracy, comparing and so on