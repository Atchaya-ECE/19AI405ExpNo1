<h1>ExpNo 1 :Developing AI Agent with PEAS Description</h1>
<h3>Name: ATCHAYA V </h3>
<h3>Register Number: 212224060031</h3>

<h3>AIM:</h3>
<p>To find the PEAS description for the given AI problem and develop an AI agent.</p>

<h3>Theory</h3>
<h3>Medicine prescribing agent:</h3>
<p>Such this agent prescribes medicine for fever (greater than 98.5 degrees) which we consider here as unhealthy, by the user temperature input, and another environment is rooms in the hospital (two rooms). This agent has to consider two factors one is room location and an unhealthy patient in a random room, the agent has to move from one room to another to check and treat the unhealthy person. The performance of the agent is calculated by incrementing performance and each time after treating in one room again it has to check another room so that the movement causes the agent to reduce its performance. Hence, agents prescribe medicine to unhealthy.</p>
<hr>
<h3>PEAS DESCRIPTION:</h3>
<table>
  <tr>
    <td><strong>Agent Type</strong></td>
    <td><strong>Performance</strong></td>
     <td><strong>Environment</strong></td>
    <td><strong>Actuators</strong></td>
    <td><strong>Sensors</strong></td>
  </tr>
    <tr>
    <td><strong>Medicine prescribing agent</strong></td>
    <td><strong>Treating unhealthy, agent movement</strong></td>
     <td><strong>Rooms, Patient</strong></td>
    <td><strong>Medicine, Treatment</strong></td>
    <td><strong>Location, Temperature of patient</strong></td>
  </tr>
</table>
<hr>
<H3>DESIGN STEPS</H3>
<h3>STEP 1:Identifying the input:</h3>
<p>Temperature from patients, Location.</p>
<h3>STEP 2:Identifying the output:</h3>
<p>Prescribe medicine if the patient in a random has a fever.</p>
<h3>STEP 3:Developing the PEAS description:</h3>
<p>PEAS description is developed by the performance, environment, actuators, and sensors in an agent.</p>
<h3>STEP 4:Implementing the AI agent:</h3>
<p>Treat unhealthy patients in each room. And check for the unhealthy patients in random room</p>
<h3>STEP 5:</h3>
<p>Measure the performance parameters: For each treatment performance incremented, for each movement performance decremented</p>

# PROGRAM:
```
import random

class MedicinePrescribingAgent:

    def __init__(self):
        self.performance = 0
        self.rooms = ["Room1", "Room2"]
        self.current_room = random.choice(self.rooms)  # Agent starts in a random room

    def sense_environment(self):
        # Randomly generate temperature between 97 and 102°F
        temperature = round(random.uniform(97, 102), 1)
        return temperature

    def prescribe_medicine(self, temperature):
        if temperature > 98.5:  # Identify unhealthy patient
            print(f"Patient in {self.current_room} has fever ({temperature}°F). Prescribing medicine.")
            self.performance += 10   # reward for treatment
        else:
            print(f"Patient in {self.current_room} is healthy ({temperature}°F). No medicine required.")

    def move_to_other_room(self):
        other_room = [room for room in self.rooms if room != self.current_room][0]
        print(f"Moving from {self.current_room} to {other_room}.")
        self.current_room = other_room
        self.performance -= 1  # movement cost

    def run_agent(self, cycles=5):
        for _ in range(cycles):
            # Sense the patient's temperature
            temp = self.sense_environment()

            # Prescribe medicine if needed
            self.prescribe_medicine(temp)

            # Move to next room
            self.move_to_other_room()

            print(f"Current Performance: {self.performance}\n")


# Run the agent
agent = MedicinePrescribingAgent()
agent.run_agent(cycles=6)
print("Final Performance Score:", agent.performance)

```
# OUTPUT:
<img width="805" height="781" alt="image" src="https://github.com/user-attachments/assets/54bf924b-64c5-4881-b3da-97a1b255f58d" />

# RESULT:
 PEAS description for the given AI problem and develop an AI agent was observed successfully.
