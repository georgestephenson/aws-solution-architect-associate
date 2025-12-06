# AWS Machine Learning Services

## Rekognition

- Detect things in images and videos
- Facial analysis and search
- Text detection
- Content moderation, detected unwanted content. Confidence threshold can be set according to confidence
- Manually review in Amazon Augmented AI (A2I)

## Transcribe

- Speech to text
- Auto-remove Personally Identifiable Information (PII) using Redaction
- Language identification
- Use cases: transcription, generate metadata to make audio searchable

## Polly

- Text to speech
- Pronunciation lexicons to specify pronunciations can be added to use in SynthesizeSpeech operation
- Speech Synthesis Markup Language (SSML) can specify how to vocalise text

## Translate

- Natural language translation

## Lex & Connect

- Lex same tech as Alexa, speech to text and recognise the intent of text
- Connect: receive calls for virtual call center
- Connect can stream to Lex, invoke a Lambda function, interact with other services etc.

## Comprehend

- Fully managed and serverless NLP
- Insights on text

### Comprehend Medical

- Detect useful information from clinical text
- Use NPM to detect Protected Health Information (PHI)

## SageMaker AI

- Fully managed service to build ML models
- e.g. train on a specific dataset to produce a desired result

## Kendra

- Document search service, index documents across different document sources to build a Knowledge Index
- Learn from user interactions which answers are preferred (Incremental Learning)

## Personalize

- Real-time personalized recommendations
- Used by Amazon.com for product recommendations
- APIs to integrate with apps, sites, emails, etc.

## Textract

- Extract text from scanned documents with AI/ML
- Extract into structured data