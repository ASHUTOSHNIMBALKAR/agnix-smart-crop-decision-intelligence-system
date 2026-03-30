[2026-03-03T10:30:00+05:30] docs: add initial project README skeleton
[2026-03-04T11:00:00+05:30] feat(ml): scaffold ml-service directory and requirements.txt
[2026-03-05T14:20:00+05:30] feat(ml): download and explore Crop Recommendation Dataset
[2026-03-06T16:45:00+05:30] feat(ml): implement train_model.py with GaussianNB classifier
[2026-03-07T09:00:00+05:30] feat(ml): achieve 99.09% accuracy on test split
[2026-03-08T11:30:00+05:30] feat(ml): serialize trained model to model.pkl using pickle
[2026-03-09T15:00:00+05:30] feat(ml): create Flask app.py with /predict POST endpoint
[2026-03-10T10:10:00+05:30] feat(ml): add CORS support to Flask microservice
[2026-03-11T13:45:00+05:30] feat(ml): return top-3 crop predictions with confidence scores
[2026-03-12T09:30:00+05:30] test(ml): add test_probs.py to verify model probabilities
[2026-03-14T11:00:00+05:30] chore: add ml-service venv to .gitignore
[2026-03-16T10:00:00+05:30] feat(backend): scaffold Node.js + Express backend with package.json
[2026-03-17T14:30:00+05:30] feat(backend): setup Express server with CORS, dotenv, mongoose
[2026-03-18T09:15:00+05:30] feat(backend): connect MongoDB via MONGO_URI environment variable
[2026-03-19T11:00:00+05:30] feat(backend): create Recommendation Mongoose schema and model
[2026-03-20T15:45:00+05:30] feat(backend): implement POST /api/recommend route
[2026-03-21T10:30:00+05:30] feat(backend): integrate axios call to ML microservice /predict
[2026-03-22T13:00:00+05:30] feat(backend): add static expectedProfitMap for 8 major crops
[2026-03-24T09:00:00+05:30] feat(backend): add getFertilizerRoadmap 3-stage helper function
[2026-03-26T11:20:00+05:30] feat(backend): add regionalBoosts map for 17 Indian states
[2026-03-27T14:00:00+05:30] feat(backend): apply +15 confidence boost for state-native crops
[2026-03-28T10:00:00+05:30] feat(backend): apply -15 confidence penalty for non-native crops
[2026-03-29T15:30:00+05:30] feat(backend): re-sort recommendations by adjusted confidence score
[2026-03-30T09:45:00+05:30] feat(backend): generate WhatsApp-ready text summary response
