"""
Project: Virtual Robot Telemetry Simulator
Author: Gauri
Description: Generates synthetic sensor logs and validates robot states for autonomous navigation.
"""

import time
import random

class TelemetrySimulator:
    def __init__(self, bot_id: str):
        self.bot_id = bot_id
        self.battery = 100
        self.is_active = True

    def run_simulation_cycle(self, cycles: int = 5):
        print(f"[{self.bot_id}] Initializing Telemetry Diagnostic...")
        
        for i in range(1, cycles + 1):
            if not self.is_active:
                break
                
            # Simulating sensor metrics
            distance = round(random.uniform(0.2, 5.0), 2)
            self.battery -= random.randint(5, 15)
            
            if self.battery <= 15:
                print(f"Cycle {i}: ⚠️ WARNING: Battery critically low at {self.battery}%. Returning to dock.")
                self.is_active = False
            elif distance < 0.5:
                print(f"Cycle {i}: 🛑 EMERGENCY: Obstacle detected at {distance}m! Applying brakes.")
            else:
                print(f"Cycle {i}: [OK] Distance to obstacle: {distance}m | Battery: {self.battery}%")
                
            time.sleep(0.5)

# Execution
if __name__ == "__main__":
    bot = TelemetrySimulator(bot_id="Satoru_Bot_v1")
    bot.run_simulation_cycle(cycles=5)
    # satoru-bot-scripts
