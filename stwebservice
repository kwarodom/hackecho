/**
 *  Web_Services
 *
 *  Copyright 2014 Warodom Khamphanchai
 *
 *  Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file except
 *  in compliance with the License. You may obtain a copy of the License at:
 *
 *      http://www.apache.org/licenses/LICENSE-2.0
 *
 *  Unless required by applicable law or agreed to in writing, software distributed under the License is distributed
 *  on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License
 *  for the specific language governing permissions and limitations under the License.
 *
 */
definition(
    name: "Web_Services",
    namespace: "Bemoss_SmartThings",
    author: "Warodom Khamphanchai",
    description: "SmartThings web services for BEMOSS",
    category: "My Apps",
    iconUrl: "https://s3.amazonaws.com/smartapp-icons/Convenience/Cat-Convenience.png",
    iconX2Url: "https://s3.amazonaws.com/smartapp-icons/Convenience/Cat-Convenience@2x.png",
    oauth: true)


preferences {
	section("Title") {
		// TODO: put inputs here
        input "switches", "capability.switch", title: "Which Switches?", multiple: true, required: false
    	input "contactSensors", "capability.contactSensor", title: "Which Contact Sensors?", multiple: true, required: false
    	input "presences", "capability.presenceSensor", title: "Which Presences?", multiple: true, required: false
		input "motionSensors", "capability.motionSensor", title: "Which Motion Sensors?", multiple: true, required: false
        input "batteries", "capability.battery", title: "Which Batteries?", multiple: true, required: false
    	input "temperatureSensors", "capability.temperatureMeasurement", title: "Which Temperature Sensors?", multiple: true, required: false
    	input "accelerations", "capability.accelerationSensor", title: "Which Acceleration Sensors?", required: false, multiple: true
        input "threeAxis", "capability.threeAxis", title: "Which threeAxis Sensors?", required: false, multiple: true
    }
}

def installed() {
	log.debug "Installed with settings: ${settings}"

	initialize()
}

def updated() {
	log.debug "Updated with settings: ${settings}"

	unsubscribe()
	initialize()
}

mappings {
  path("/switches") {
    action: [
      GET: "listSwitches",
      PUT: "updateSwitches"
    ]
  }
  path("/switches/:id") {
    action: [
      GET: "showSwitch",
      PUT: "updateSwitch"
    ]
  }
  path("/contactSensors") {
    action: [
      GET: "listContactSensors"
    ]
  }
  path("/contactSensors/:id") {
    action: [
      GET: "showContactSensor"
    ]
  }
  path("/presences") {
    action: [
      GET: "listPresences"
    ]
  }
  path("/presences/:id") {
    action: [
      GET: "showPresence"
    ]
  }
  path("/motions") {
    action: [
      GET: "listMotions"
    ]
  }
  path("/motions/:id") {
    action: [
      GET: "showMotion"
    ]
  }
  path("/batteries") {
    action: [
      GET: "listBatteries"
    ]
  }
  path("/batteries/:id") {
    action: [
      GET: "showBattery"
    ]
  }
  path("/temperatures") {
    action: [
      GET: "listTemperatureSensors"
    ]
  }
  path("/temperatures/:id") {
    action: [
      GET: "showTemperatureSensor"
    ]
  }
  path("/accelerations") {
    action: [
      GET: "listAccelerationSensors"
    ]
  }
  path("/accelerations/:id") {
    action: [
      GET: "showAccelerationSensor"
    ]
  }
  path("/threeaxis") {
    action: [
      GET: "listThreeAxisSensors"
    ]
  }
  path("/threeaxis/:id") {
    action: [
      GET: "showThreeAxisSensor"
    ]
  }
}

def listSwitches() {
	switches
}
 
def showSwitch() {
	showS(switches.find{it.id == params.id}, "switch")
}

private showS(device, type) {
	def attributeName = type
	def s = device.currentState("switch")
    def k = device.currentState("power")
	[label: device.displayName, status: s?.value, unitTime: s?.date?.time, type: type, power: k?.value,]
}

void updateSwitch() {
    def command = request.JSON?.command
    if (command) {
      def mySwitch = switches.find { it.id == params.id }
      if (!mySwitch) {
        httpError(404, "Switch not found")
      } else {
        mySwitch."$command"()
      }
    }
}

def listContactSensors() {
	contactSensors
}

def showContactSensor() {
	showC(contactSensors.find{it.id == params.id}, "contactSensor")
}

private showC(device, type) {
	def attributeName = "contact"
	def s = device.currentState(attributeName)
	[label: device.displayName, contact: s?.value, unitTime: s?.date?.time, type: type]
}

def listPresences() {
	presences
}

def showPresence() {
	showP(presences.find{it.id == params.id}, "presenceSensor")
}

private showP(devices, type) {
	def attributeName = type
	def s = devices.currentState("presence")
	[label: devices.displayName, presence: s?.value, unitTime: s?.date?.time, type: type,]
}

def listMotions() {
	motionSensors
}

def showMotion() {
	showM(motionSensors.find{it.id == params.id}, "motionSensor")
}

private showM(devices, type) {
	def attributeName = type
	def s = devices.currentState("motion")
	[label: devices.displayName, motion: s?.value, unitTime: s?.date?.time, type: type,]
}

def listBatteries() {
	batteries
}

def showBattery() {
	showB(batteries.find{it.id == params.id}, "battery")
}

private showB(devices, type) {
	def attributeName = type
	def s = devices.currentState("battery")
	[label: devices.displayName, battery: s?.value, unitTime: s?.date?.time, type: type,]
}

def listTemperatureSensors() {
	temperatureSensors
}

def showTemperatureSensor() {
	showT(temperatureSensors.find{it.id == params.id}, "temperatureMeasurement")
}

private showT(devices, type) {
	def attributeName = type
	def s = devices.currentState("temperature")
	[label: devices.displayName, temperature: s?.value, unitTime: s?.date?.time, type: type,]
}

def listAccelerationSensors() {
	log.debug "listAccelerationSensors is called"
    log.debug "$accelerations"
	accelerations
}

def showAccelerationSensor() {
	showA(accelerations.find{it.id == params.id}, "accelerationSensor")
}

private showA(devices, type) {
	def attributeName = type
	def s = devices.currentState("acceleration")
	[label: devices.displayName, acceleration: s?.value, unitTime: s?.date?.time, type: type,]
}

def listThreeAxisSensors() {
	threeAxis
}

def showThreeAxisSensor() {
	showThree(threeAxis.find{it.id == params.id}, "threeAxis")
}

private showThree(devices, type) {
	def attributeName = type
	def s = devices.currentState("threeAxis")
	[label: devices.displayName, threeAxis: s?.value, unitTime: s?.date?.time, type: type,]
}

def initialize() {
	// TODO: subscribe to attributes, devices, locations, etc.
    if (!state.accessToken)
    	createAccessToken()
    log.trace "Token: $state.accessToken - App ID: $app.id"
}

// TODO: implement event handlers
