# Records Request Triage

A prototype built for my AI for Impact application. It helps a city records team triage incoming public records requests.

**Live demo** https://tejashiv.github.io/records-request-triage

## What it does

Paste a public records request and it

- suggests which department should handle it, with a confidence level
- shows the similar past requests behind that suggestion
- flags sensitive topics such as personnel files, law enforcement records and minors for legal review
- shows the response deadline
- checks whether the record is already published, so staff can point the requester there
- asks for clarification instead of guessing when a request is too vague

Staff accept or correct every suggestion, and each correction is logged.

## How it works

Requests are matched against past requests with BM25 keyword scoring plus a small synonym table. The suggested department is a weighted vote of the five most similar past requests, and confidence is the share of that vote the top department won. Suggestions below 60 percent confidence, weak matches and sensitive topics always go to a person.

This follows the retrieval approach from my patent search engine. A production version would add embeddings and cross encoder reranking, while keeping routing based on precedent, because precedent is easy for staff to check.

## What it never does

It never denies, withholds or redacts a record, and it never replies to a requester. It runs entirely in the browser, so nothing typed is sent anywhere.

## Data

Every request and record in this demo is synthetic, written for the prototype. Real request logs often contain residents' personal details, so they were deliberately kept out of a public demo.

## How it was built

I designed and tested this with Claude, which wrote much of the code. My testing caught a rule that wrongly rejected short, specific requests such as "officer discipline" as too vague, and I had it fixed.
