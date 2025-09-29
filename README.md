<h1>ExpNo 1 :Developing AI Agent with PEAS Description</h1>
<h3>Name: ATCHAYA V </h3>
<h3>Register Number: 2122240660031</h3>

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

class HealthMonitoringAgent:
    def __init__(self, patient_data):
        self.patient_data = patient_data

    def monitor_health(self):
        while True:
            current_health_state = self.sensors.get_health_state()
            action = self.choose_action(current_health_state)
            self.actuators.perform_action(action)
            if self.choose_action(current_health_state)=="No specific action needed":
                break

    def choose_action(self, current_health_state):
        # Example: A simple rule-based system for decision-making
        if current_health_state['heart_rate'] > 120:
            return "Alert healthcare provider: High heart rate detected"
        elif current_health_state['blood_pressure'] > 140:
            return "Alert healthcare provider: High blood pressure detected"
        elif current_health_state['temperature'] > 38:
            return "Recommend rest and monitor temperature"
        else:
            return "No specific action needed"

class HealthSensors:
    def get_health_state(self):
        # Example: Simulate health data retrieval (replace with real data in a practical scenario)
        return {
            'heart_rate': random.randint(60, 150),
            'blood_pressure': random.randint(90, 160),
            'temperature': random.uniform(36.0, 38.5)
        }

class HealthActuators:
    def perform_action(self, action):
        # Example: Print or log the action (in a real scenario, this might involve more complex actions)
        print(action)

if __name__ == "__main__":
    patient_data = {'patient_id': 123, 'name': 'John Doe', 'age': 35}
    
    health_sensors = HealthSensors()
    health_actuators = HealthActuators()
    
    health_monitoring_agent = HealthMonitoringAgent(patient_data)
    health_monitoring_agent.sensors = health_sensors
    health_monitoring_agent.actuators = health_actuators
    
    health_monitoring_agent.monitor_health()
```
# OUTPUT:
```
{
 "cells": [
  {
   "cell_type": "code",
   "execution_count": 25,
   "id": "cbbf181b",
   "metadata": {},
   "outputs": [],
   "source": [
    "import random\n",
    "import time\n",
    "\n",
    "\n",
    "class Thing: \n",
    "    \"\"\"\n",
    "    This represents any physical object that can appear in an Environment. \"\"\"\n",
    "\n",
    "    def is_alive(self):\n",
    "        \"\"\"Things that are 'alive' should return true.\"\"\"\n",
    "        return hasattr(self, \"alive\") and self.alive\n",
    "\n",
    "    def show_state(self):\n",
    "        \"\"\"Display the agent's internal state. Subclasses should override.\"\"\"\n",
    "        print(\"I don't know how to show_state.\")"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 26,
   "id": "068fa3ac",
   "metadata": {},
   "outputs": [],
   "source": [
    "class Agent(Thing):\n",
    "    \n",
    "    \"\"\"\n",
    "        An Agent is a subclass of Thing \"\"\"\n",
    "\n",
    "    def __init__(self, program=None):\n",
    "        self.alive = True\n",
    "        self.performance = 0 \n",
    "        self.program = program\n",
    "\n",
    "    def can_grab(self, thing):\n",
    "        \"\"\"Return True if this agent can grab this thing. Override for appropriate subclasses of Agent and Thing.\"\"\" \n",
    "        return False"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 27,
   "id": "c4f0bfac",
   "metadata": {},
   "outputs": [],
   "source": [
    "def TableDrivenAgentProgram(table): \n",
    "    \"\"\"\n",
    "    [Figure 2.7]\n",
    "    This agent selects an action based on the percept sequence. It is practical only for tiny domains.\n",
    "    To customize it, provide as table a dictionary of all\n",
    "    {percept_sequence:action} pairs. \"\"\"\n",
    "    percepts = []\n",
    "    \n",
    "\n",
    "    def program(percept):\n",
    "        action = None\n",
    "        percepts.append(percept)\n",
    "        action = table.get(tuple(percepts))\n",
    "        return action \n",
    "    return program\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 41,
   "id": "b36f34b8",
   "metadata": {},
   "outputs": [],
   "source": [
    "room_A, room_B = (0,0), (1,0) # The two locations for the Doctor to treat"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 42,
   "id": "e5a5e703",
   "metadata": {},
   "outputs": [],
   "source": [
    "def TableDrivenDoctorAgent():\n",
    "    \"\"\"\n",
    "    Tabular approach towards hospital function. \n",
    "    \"\"\"\n",
    "        \n",
    "    table = {\n",
    "    ((room_A, \"healthy\"),): \"Right\",\n",
    "    ((room_A, \"unhealthy\"),): \"treat\",\n",
    "    ((room_B, \"healthy\"),): \"Left\",\n",
    "    ((room_B, \"unhealthy\"),): \"treat\",\n",
    "    ((room_A, \"unhealthy\"), (room_A, \"healthy\")): \"Right\",\n",
    "    ((room_A, \"healthy\"), (room_B, \"unhealthy\")): \"treat\",\n",
    "    ((room_B, \"healthy\"), (room_A, \"unhealthy\")): \"treat\",\n",
    "    ((room_B, \"unhealthy\"), (room_B, \"healthy\")): \"Left\",\n",
    "    ((room_A, \"unhealthy\"), (room_A, \"healthy\"), (room_B, \"unhealthy\")): \"treat\",\n",
    "    ((room_B, \"unhealthy\"), (room_B, \"healthy\"), (room_A, \"unhealthy\")): \"treat\",\n",
    "    }\n",
    "    return Agent(TableDrivenAgentProgram(table))\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 43,
   "id": "f43f8c9d",
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "<__main__.Agent at 0x20b18d2bc50>"
      ]
     },
     "execution_count": 43,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "TableDrivenDoctorAgent()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "id": "09662dbb",
   "metadata": {},
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "code",
   "execution_count": 54,
   "id": "85f47933",
   "metadata": {},
   "outputs": [],
   "source": [
    "class Environment:\n",
    "    \"\"\"Abstract class representing an Environment. 'Real' Environment classes inherit from this. Your Environment will typically need to implement:\n",
    "    percept:\tDefine the percept that an agent sees. execute_action:\tDefine the effects of executing an action.\n",
    "    Also update the agent.performance slot.\n",
    "    The environment keeps a list of .things and .agents (which is a subset of .things). Each agent has a .performance slot, initialized to 0.\n",
    "    Each thing has a .location slot, even though some environments may not need this.\"\"\"\n",
    "\n",
    "    def __init__(self):\n",
    "        self.things = [] \n",
    "        self.agents = []\n",
    "        #room_A, room_B = (0,0), (1,0) # The two locations for the Doctor to treat\n",
    "\n",
    "    def percept(self, agent):\n",
    "        \"\"\"Return the percept that the agent sees at this point. (Implement this.)\"\"\"\n",
    "        raise NotImplementedError\n",
    "\n",
    "    def execute_action(self, agent, action):\n",
    "        \"\"\"Change the world to reflect this action. (Implement this.)\"\"\" \n",
    "        raise NotImplementedError\n",
    "\n",
    "    def default_location(self, thing):\n",
    "        \"\"\"Default location to place a new thing with unspecified location.\"\"\"\n",
    "        return None\n",
    "\n",
    "    def is_done(self):\n",
    "        \"\"\"By default, we're done when we can't find a live agent.\"\"\" \n",
    "        return not any(agent.is_alive() for agent in self.agents)\n",
    "\n",
    "    def step(self):\n",
    "        \"\"\"Run the environment for one time step. If the\n",
    "        actions and exogenous changes are independent, this method will do. If there are interactions between them, you'll need to override this method.\"\"\"\n",
    "        if not self.is_done(): \n",
    "            actions = []\n",
    "            for agent in self.agents:\n",
    "                if agent.alive:\n",
    "                    actions.append(agent.program(self.percept(agent))) \n",
    "                else:\n",
    "                    actions.append(\"\")\n",
    "            for (agent, action) in zip(self.agents, actions): \n",
    "                self.execute_action(agent, action)\n",
    "\n",
    "    def run(self, steps=1000):\n",
    "        \"\"\"Run the Environment for given number of time steps.\"\"\"\n",
    "        for step in range(steps):\n",
    "            if self.is_done():\n",
    "                return \n",
    "            self.step()\n",
    "\n",
    "    def add_thing(self, thing, location=None):\n",
    "        \"\"\"Add a thing to the environment, setting its location. For convenience, if thing is an agent program we make a new agent for it. (Shouldn't need to override this.)\"\"\"\n",
    "        if not isinstance(thing, Thing):\n",
    "            thing = Agent(thing)\n",
    "        if thing in self.things:\n",
    "            print(\"Can't add the same thing twice\") \n",
    "        else:\n",
    "            thing.location = (location if location is not None else self.default_location(thing))\n",
    "            self.things.append(thing) \n",
    "            if isinstance(thing, Agent):\n",
    "                thing.performance = 0 \n",
    "                self.agents.append(thing)\n",
    "\n",
    "    def delete_thing(self, thing):\n",
    "        \"\"\"Remove a thing from the environment.\"\"\"\n",
    "        try:\n",
    "            \n",
    "            self.things.remove(thing) \n",
    "        except ValueError as e:\n",
    "            print(e)\n",
    "            print(\" in Environment delete_thing\")\n",
    "            print(\" Thing to be removed: {} at {}\".format(thing, thing.location))\n",
    "            print(\" from list: {}\".format([(thing, thing.location) for thing in self.things]))\n",
    "        if thing in self.agents: \n",
    "            self.agents.remove(thing)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 55,
   "id": "7ec19095",
   "metadata": {},
   "outputs": [],
   "source": [
    "\n",
    "class TrivialDoctorEnvironment(Environment):\n",
    "    \"\"\"This environment has two locations, A and B. Each can be unhealthy or healthy. The agent perceives its location and the location's status. This serves as an example of how to implement a simple Environment.\"\"\"\n",
    "\n",
    "    def __init__(self):\n",
    "        super().__init__()\n",
    "        #room_A, room_B = (0,0), (1,0) # The two locations for the Doctor to treat\n",
    "        self.status = {room_A: random.choice([\"healthy\", \"unhealthy\"]), room_B: random.choice([\"healthy\", \"unhealthy\"]),}\n",
    "\n",
    "    def thing_classes(self):\n",
    "        return [TableDrivenDocterAgent]\n",
    "\n",
    "    def percept(self, agent):\n",
    "        \"\"\"Returns the agent's location, and the location status (unhealthy/healthy).\"\"\"\n",
    "        return agent.location, self.status[agent.location]\n",
    "\n",
    "    def execute_action(self, agent, action):\n",
    "        \"\"\"Change agent's location and/or location's status; track performance. Score 10 for each treatment; -1 for each move.\"\"\"\n",
    "        if action == \"Right\":\n",
    "            agent.location = room_B\n",
    "            agent.performance -= 1\n",
    "        elif action == \"Left\":\n",
    "            agent.location = room_A\n",
    "            agent.performance -= 1\n",
    "        elif action == \"treat\":\n",
    "            tem=float(input(\"Enter your temperature\")) \n",
    "            if tem>=98.5:\n",
    "                self.status[agent.location] == \"unhealthy\"\n",
    "                print(\"medicine prescribed: paracetamol and anti-biotic(low dose)\")\n",
    "                agent.performance += 10\n",
    "            else:\n",
    "                self.status[agent.location] = \"healthy\" \n",
    "            self.status[agent.location] = \"healthy\"\n",
    "\n",
    "\n",
    "    def default_location(self, thing):\n",
    "           \n",
    "        return random.choice([room_A, room_B])"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 59,
   "id": "0a39a340",
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "\tStatus of patients in rooms before treatment\n",
      "{(0, 0): 'unhealthy', (1, 0): 'healthy'}\n",
      "AgentLocation : (1, 0)\n",
      "Performance : 0\n",
      "\n",
      "\tStatus of patient in room after the treatment\n",
      "{(0, 0): 'unhealthy', (1, 0): 'healthy'}\n",
      "AgentLocation : (0, 0)\n",
      "Performance : -1\n",
      "Enter your temperature100\n",
      "medicine prescribed: paracetamol and anti-biotic(low dose)\n",
      "\n",
      "\tStatus of patient in room after the treatment\n",
      "{(0, 0): 'healthy', (1, 0): 'healthy'}\n",
      "AgentLocation : (0, 0)\n",
      "Performance : 9\n"
     ]
    }
   ],
   "source": [
    "if   __name__ == \"__main__\":\n",
    "    \n",
    "    agent = TableDrivenDoctorAgent() \n",
    "    environment = TrivialDoctorEnvironment() \n",
    "    #print(environment)\n",
    "    environment.add_thing(agent)\n",
    "    print(\"\\tStatus of patients in rooms before treatment\")\n",
    "    print(environment.status)\n",
    "    print(\"AgentLocation : {0}\".format(agent.location)) \n",
    "    print(\"Performance : {0}\".format(agent.performance))\n",
    "    time.sleep(3)\n",
    "    for i in range(2):\n",
    "        environment.run(steps=1)\n",
    "        print(\"\\n\\tStatus of patient in room after the treatment\") \n",
    "        print(environment.status)\n",
    "        print(\"AgentLocation : {0}\".format(agent.location)) \n",
    "        print(\"Performance : {0}\".format(agent.performance)) \n",
    "        time.sleep(3)"
   ]
  }
 ],
 "metadata": {
  "kernelspec": {
   "display_name": "Python 3 (ipykernel)",
   "language": "python",
   "name": "python3"
  },
  "language_info": {
   "codemirror_mode": {
    "name": "ipython",
    "version": 3
   },
   "file_extension": ".py",
   "mimetype": "text/x-python",
   "name": "python",
   "nbconvert_exporter": "python",
   "pygments_lexer": "ipython3",
   "version": "3.11.5"
  }
 },
 "nbformat": 4,
 "nbformat_minor": 5
}
```
# RESULT:
 PEAS description for the given AI problem and develop an AI agent was observed successfully.
