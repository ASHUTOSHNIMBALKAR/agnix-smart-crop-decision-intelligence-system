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
[2026-03-31T11:00:00+05:30] feat(backend): save enriched recommendation record to MongoDB
[2026-04-01T10:00:00+05:30] feat(backend): implement GET /api/weather with simulated data
[2026-04-02T13:30:00+05:30] test(backend): add test.js API integration test script
[2026-04-04T09:00:00+05:30] feat(frontend): scaffold React + Vite project with npm create
[2026-04-05T11:00:00+05:30] feat(frontend): configure vite.config.js and eslint
[2026-04-06T14:00:00+05:30] feat(frontend): create App.jsx root component with state management
[2026-04-07T10:30:00+05:30] feat(frontend): build RecommendationForm component with all input fields
[2026-04-08T15:00:00+05:30] feat(frontend): add soil NPK, pH, moisture and soil type dropdowns
[2026-04-09T09:30:00+05:30] feat(frontend): add weather inputs: temperature, humidity, rainfall
[2026-04-10T11:45:00+05:30] feat(frontend): add water availability and season selector inputs
[2026-04-11T14:00:00+05:30] feat(frontend): add state/region selector for regional crop boost
[2026-04-13T10:00:00+05:30] feat(frontend): build ResultsDisplay component for top-3 crop cards
[2026-04-14T13:30:00+05:30] feat(frontend): display confidence score, profit and fertilizer info
[2026-04-16T09:00:00+05:30] feat(frontend): implement pdfGenerator.js utility with jsPDF
[2026-04-17T11:30:00+05:30] feat(frontend): add Download PDF button to ResultsDisplay
[2026-04-18T14:15:00+05:30] style(frontend): add App.css responsive mobile-first design
[2026-04-20T10:00:00+05:30] style(frontend): add loading spinner and disabled state on submit
[2026-04-22T09:30:00+05:30] fix(backend): handle missing location field gracefully in recommend
