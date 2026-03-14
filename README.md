from fastapi import FastAPI
from pydantic import BaseModel
from typing import Optional

app = FastAPI(title="ArogyaMitra AI")

class UserProfile(BaseModel):
    age: int
    weight: float  # in kg
    goal: str      # e.g., "muscle gain", "weight loss"
    activity_level: str

@app.get("/")
def home():
    return {"message": "Welcome to ArogyaMitra Health Agent API"}

@app.post("/generate-plan")
async def create_workout(profile: UserProfile):
    # This is where your AI Logic (e.g., Gemini or OpenAI) would go
    # For now, we'll simulate a simple logic response
    bmi = profile.weight / (1.75 ** 2)  # Simplified constant height
    
    plan = {
        "status": "success",
        "calculated_bmi": round(bmi, 2),
        "recommendation": f"Based on your goal of {profile.goal}, we suggest a 4-day split."
    }
    return plan

if __name__ == "__main__":
    import uvicorn
    uvicorn.run(app, host="0.0.0.0", port=8000)
