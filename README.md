## Introduction
The PaMEAS Evacuation Policy is part of the PaMEAS (Passenger Mustering and Evacuation Process Automation) integrated system which was developed in the context of the PALAEMON project. Specifically this policy defines the evacuation of a ship as a process with seven distinct **Evacuation Phases**. Each phase defines one or more **Evacuation Tasks** that must be executed by the passengers and/or crew members. The PaMEAS Evacuation Policy maps each such task to a (set of possibly empty) **message objects** (depending on whether the task is a messaging task or not) that specify the messages that must be communicated to the passengers and/or crew members. Essentially, these message objects are produced by executing in the current context the rules defining the policy. The result of this execution is the generation of the messages that need to be delivered to the passengers and crew (recipients, type of messages, communication channel, content and so on) instructing them to implement the various evacuation tasks. 

PaMEAS Evacuation Messaging Policy is formalised as a set of Event Condition Action (ECA) rules that specify what actions a given subject (passenger or crew of the ship) should take on a given evacuation phase based on the passenger identity profile and health-status information, their location and the availability of evacuation routes; as well as on eventual incidents (for example, passengers locked in a cabin) that may occur during the evacuation process which require the intervention of the crew.

This policy is communicated directly to passengers’ and crew personal devices (e.g. mobile phones, smart bracelets, smartwatches, etc.) via easy to read and comprehend messages, alerts, warnings and notifications, in the form of simple text messages but also as audio-visual communication (*examples:* “The designated evacuation route to Master Station 1 has been blocked. Follow the alternative path below. (passengers and crew), or “Move to designated emergency posts “(crew)) via PaMEAS.

## PaMEAS Evacuation Messaging Policy
To formalise the evacuation policy we use the concept of a Policy Rule. Each rule is an Event Condition Action (ECA) rule that has three parts. One is the event which when detected triggers the rule, another is the condition which if it holds it fires the execution of the rule and the application of its action (third part). The rules can be combined into rule sets with logical connectives. One or more rule sets form a rule family and one or more rule families form the policy. 

After analysing the respective literature and consulting with industry experts, our evacuation policy defines four main family of rules that are used to express its purpose:

**RF1:** The first rule family consists of one ruleset and its purpose is to define the evacuation profile of the passengers based on their health data.

**RF2:** The second rule family consists of two rulesets and its purpose is to define the evacuation path the passengers must follow based on their location and the status of the evacuation routes.

**RF3:** The third rule family consists of one ruleset and its purpose is to compose the message objects of each evacuation task based on the evacuation phase and the emergency information that needs to be communicated under each task.

**RF4:** The fourth rule family consists of two rulesets and its purpose is to define the body of the message object (including any auxiliary files, e.g. picture of evacuation paths, etc.) to be sent during the evacuation phases of the ship to the passengers and crew: 
The first rule set defines the messages addressed to the crew.
The second rule set defines the messages addressed to the passengers of the ship.

In detail, the first rule family is defined as follows:

**Definition 1 (RF1 - Evacuation profile ruleset).** *Assume a system state S and a detected event by the system E. RuleFamily1(S, E) consists of one rule set of Event Condition Action (ECA) rules of the form ON event IF condition THEN DO action, defined as follows*:
```
ECA(
ON(Evacuation_Phase_4_Start_event)
IF(getPerson(S) = p /\ p.getType() == Passenger /\
p.getMedicalAssistance() \in SET_OF_MEDICAL_ASSISTANCE /\ p.getMobilityIssues() \in SET_OF_MOBILITY_ISSUES /\ p.getPregnancyData() \in SET_OF_PREGRANCY_DATA)
THEN DO(AssignType(p, assingment_type) /\ assignment_type \in SET_OF_ASSIGNMENT_TYPE)
)
```

In this definition:

*Evacuation_Phase_4_Start_event \in SET_of_Defined_Events* which is a set of predefined events that change the system state 

*Evacuation_Phase_4_Start_event* denotes the start event of the evacuation phase 4, i.e. the launch of the evacuation protocol
p is a constant of type Person

*getPerson: S -> Person* is a function that takes as input a state of the system and returns the person of that state 

*getType : Person -> pType* is a function that takes as input an element of type Person and returns his type, an element of the set {“Crew”, “Passenger”}

*getMedicalAssistance: Person -> SET_OF_MEDICAL_ASSISTANCE* is a function that takes as input an element of type Person and returns an element of the set {“equip_required”, “stretcher”, “heavy_doses”, “none”} that denotes whether the person requires medical assistance during evacuation or not (requires medical equipment during evacuation, requires a stretcher, receives medication affecting their ability to complete the evacuation process safely without assistance or is able to evacuate unassisted, respectively).

*getMobilityStatus: Person -> SET_OF_MOBILITY_ISSUES* is a function that takes as input an element of type Person and returns an element of the set {"assisted_gait","walking_disability",”severe_walking_disability”,”unable_to_walk”,
 ”visually_impaired”,”hearing_impaired”,”cognitive_impaired”, "none"} that denotes whether the person has any mobility issue or not (requires walking cane, frame, or crutches to move to the assembly station, requires wheelchair to move to the assembly station, requires wheelchair to move to the assembly station and must be carried up/down steps, is unable to walk, has impairments that may affect his mobility, or no mobility problems, respectively.
 
*getPregnancyStatus: Person -> SET_OF_PREGRANCY_DATA* is a function that takes as input an element of type Person and returns an element of the set{"complicated”, “normal”} that denotes the pregnancy status of that person

*AssignType: Person -> SET_OF_ASSIGNMENTS* is a function that takes as input an element of type Person and assigns to that person an element of the set {“follow path”, “wait help”} denoting whether that person can follow the instructions received in their personal devices or needs personal assistance by the crew to evacuate.

Additionally:

*getAssignType: Person->Assignment* is a function that takes as input a person and returns his assignment type.

Essentially, the Evacuation profile ruleset is triggered after the launch of the evacuation protocol (event) and defines the passenger’s evacuation profile (action) based on their health data (condition) by categorising them as being able to follow the instructions of the messages delivered to them or need help to evacuate by a crew member.

The second rule family is defined as follows:

**Definition 2 (RF2).** *Assume a system state S and a detected event by the system E. RuleFamily_2(S, E) consists of two rule sets of Event Condition Action (ECA) rules of the form ON event IF condition THEN DO action, defined as follows:*

**Definition 2.1 (RS2.1 - Evacuation path ruleset):** *The Evacuation path ruleset is defined as follows:*

```
ECA(
ON(Evacuation_profile_completed)
IF(getPerson(S) = p /\ p.getType() == Passenger /\ getGeofence(S,p) == g /\ getAssignMSpath(p) == none /\ getStatusMSPath(S,MSpath) == free)
THEN DO(AssignMSpath(p,MSpath)) 
)
```

In this definition:

*Evacuation_profile_completed \in SET_of_Defined_Events* which is a set of predefined events that change the system state

*Evacuation_profile_completed event* denotes the completion of the evacuation profiles of the passengers 

*p* is a constant of type *Person*

*getPerson: S -> Person* is a function that takes as input a state of the system and returns the person of the state 

*getType: Person -> pType* is a function that takes as input an element of type Person and returns his type, an element of the set {“Crew”, “Passenger”}
g is a constant of type Geofence

*getGeofence: Person State -> Geofence* is a function that takes as input an element of type Person and returns the geofence of the ship in which the person is currently located 

*getAssignMSpath: Person -> Pat*h  is a function that takes as input a Person and returns the path to the assigned Master Station of that person 

*getStatusMSPath: State Path -> Status* is a function that takes as input a state and a path to a Master Station and returns an element of the set {free, blocked} denoting the current status of the path to the master station

*AssignMSpath: Person -> SET_OF_MS_PATHS* is a function that takes as input an element of type Person and assigns a path and a Master Station to that person 

Additionally:

*getPathDescription: Path -> PathDescription* is a function that takes as input a Path and returns the description of it, i.e. instructions in order to follow this path

*getPathImage: Path -> Image* is a function that takes as input a Path and returns an image with a map of this path 

Essentially, the Evacuation path profile ruleset is triggered after the completion of the evacuation profiles of the passengers (event) and defines each passenger’s mustering path (action) based on their current location and the status of the paths (condition) by assigning to the passenger a Master Sation and a Path to the Master Station. 

The second ruleset is defined as;
**Definition 2.2 (RS2.2 - Update Evacuation path ruleset):** *The Update Evacuation path ruleset is defined as follows:*
```
ECA(
ON(Evacuation_profile_completed and GeoFence_status_update)
IF(getPerson(S) = p /\ p.getType() == Passenger /\ getStatusMSPath(S,getAssignMSpath(p)) == blocked /\ p.getGeofence() =/= p.getAssignMS())
THEN DO (AssignMSpath(p,getAltPath(getAssignMSpath(p),getBlockedGeofence(S,getAssignMSpath(p)))))
)
```
In this definition:

*GeoFence_status_update \in SET_of_Defined_Events* which is a set of predefined events that change the system state.

*GeoFence_status_update event* denotes that the status of the geofences has changed.

*p* is a constant of type *Person*.

*getPerson: State -> Person* is a function that takes as input a state of the system and returns the person of the state.

*getType: Person -> pType* is a function that takes as input an element of type Person and returns his type, an element of the set {“Crew”, “Passenger”}

*getAssignMSpath: Person -> Path*  is a function that takes as input a Person and returns the path to the assigned Master Station of that person 

*getStatusMSPath: State Path -> Status* is a function that takes as input a state and a path to a Master Station and returns an element of the set {free, blocked} denoting the current status of the path to the master station

*getBlockedGeofence: State Path -> Geofence* is a function that takes as input a state and a path to a Master Station and returns the blocked geofences of this path

*gi* is a constant of type Geofence

*getGeofence: Person State -> Geofence* is a function that takes as input an element of type Person and returns the geofence of the ship in which the person is currently located.

*getAssignMS: Person -> MasterStation*  is a function that takes as input a Person and returns the Assigned Master Station of that person (last element of the MSpath)

*AssignMSpath: Person -> SET_OF_MS_PATHS* is a function that takes as input an element of type Person and assigns to that person a Master Station and a path to the Assigned Master Station

*getAltPath: Path Geofence -> Path* is a function that takes as input a path and the blocked geofences of the path and returns an alternative path for the same destination

Essentially, the Update Evacuation path profile ruleset is triggered when the status of one or more geofences changes due to the evolution of the emergency (event) and if the geofences of a Passenger’s path to his master station become blocked and he hasn’t arrived to his Master Station yet (condition) it basically re-assigns a path (and/or a master station) to him (action).

The third rule family is defined as follows:

**Definition 3 (RF3 - Message object composition ruleset).** *Assume a system state S and a detected event by the system E. RuleFamily_3(S, E) consists of one rule set of Event Condition Action (ECA) rules of the form ON event IF condition THEN DO action, defined as follows: *
```
ECA(
ON(Evacuation_Phase_i_Start_event)
IF(getEvacuationTask(S) = t /\ t.getType() == tType /\ tType \in SET_OF_tTYPE)
THEN DO(
ComposeMessageObject(t)/\ SetMessagetype(m, message_type) /\ message_type \in SET_OF_MESSAGE_TYPE /\ SetMessageSender(m, message_sender) /\ message_sender \in SET_OF__SENDER /\ SetMessageAudience(m, message_audience) /\ message_audience \in SET_OF__AUDIENCE /\ SetMessageLayout(m, message_layout) /\ message_layout \in SET_OF__LAYOUT /\ SetMessageChannel(m, message_channel) /\ message_channel \in SET_OF__CHANNEL /\ SetMessageBody(p, m, empty)/\ SetMessageFile(p, m, none)/\
)
```
In this definition:

*Evacuation_Phase_i_Start_event, i = 1, … , 8 \in SET_of_Defined_Events*, which is a set of predefined events that when detected change the state of the system

*Evacuation_Phase_i_Start_event, i = 1, … , 8* denote the start events of the eight evacuation phases 

*t* is a constant of type *Task*

*getEvacuationTask: S -> Task* is a function that takes as input a state of the system and returns the evacuation process task of that state 

*getType: Task -> tType* is a function that takes as input an element of type Task and returns his type, an element of the set {“Messaging”, “NoMessaging”}

*ComposeMessageObject: Task -> MessageObject* is a function that takes as input an element of type Task and composes the message object of this task
m is a constant of type MessageObject

*SetMessageType: MessageObject Messagetype-> MessageObject* is a function that takes as input an element of type MessageObject and an element of the set {“Alert”, “Warning”, “Notifications”, "Feedback message", "Communication Session"} and creates the message type of the message object

*SetMessageSender: MessageObject MessageSender -> MessageObject*  is a function that takes as input an element of type MessageObject and an element of the set {“Crew”, “Evacuation Coordinator”, "PaMEAS"} and creates the message sender of the message object

*SetMessageAudience: MessageObject MessageAudience -> MessageObject*  is a function that takes as input an element of type MessageObject and an element of the set {“Crew”, “Passengers”, "Crew Managers", "Evacuation Coordinator", "PaMEAS"} and creates the audience of the message object

*SetMessageLayout: MessageObject MessageLayout -> MessageObject* is a function that takes as input an element of type MessageObject and an element of the set {“text", "visual", "voice", "vibration", video”} and creates the layout of the message object

*SetMessageChannel: MessageObject MessageChannel -> MessageObject*  is a function that takes as input an element of type MessageObject and an element of the set {“Task Management Service”, “Evacuation Management Service”} and creates the delivery channel of the message object

*SetMessageBody: Person MessageObject MessageBody -> MessageObject* is a function that takes as input a person, a message object and a message body and creates the message body of the message object addressed to that person

*SetMessageFile: Person MessageObject File -> MessageObject* is a function that takes as input a person, a message object and a file and includes it to the message object addressed to that person

*Empty* is a constant denoting an empty message body.

*None* is a constant denoting that there is no auxiliary file included it in the message object.

The Message object composition ruleset essentially checks in which evacuation phase the system is (event) and based on the evacuation process task that needs to be executed (condition) composes the message objects of the task (action). The message object of each evacuation task contains the basic characteristics of the messages (type, sender, audience, layout and delivery channel) that will be disseminated during this evacuation task. The body of the message object and any additional files it may contain will be defined based on the recipients’ personalised profiles and the evacuation process task.

The fourth rule family is defined as follows:

**Definition 4 (RF4).** *Assume a system state S and a detected event by the system E. RuleFamily_3(S, E) consists of two rule sets of Event Condition Action (ECA) rules of the form ON event IF condition THEN DO action, defined as follows;*

**Definition 4.1 (RS4.1 - Passenger Message creation ruleset):** *The Passenger Message creation ECA ruleset is defined as:*
```
ECA(
ON(Message_Object_Composition_Completed)
IF(getMessageObject(S) = m /\ m =/= empty
/\ m.getMessageAudience() == Passenger 
/\ getPerson(S) = p /\ p.getType() == Passenger /\ p.getLanguage() == pLanguage /\ pLanguage \in SET_OF_LANGUAGE /\ p.getAssignType() == assignment_type /\ assignment_type \in SET_OF_ASSIGNMENT_TYPE /\ p.getMobilityStatus == mobility_issue /\ mobility_issue \in SET_OF_MOBILITY_ISSUES)
THEN DO(SetMessageBody(p, o, message_body) /\ message_body \in String /\ SetMessageFile(p, o, file) /\ file \in SET_OF_FILE /\ SendMessage(p, o)
)
```
In this definition:

*Message_Object_Composition_Completed \in SET_of_Defined_Events*, which is a set of predefined events that when detected change the state of the system

*Message_Object_Composition_Completed* denotes the completion of the message object composition phase 

*getMessageObject : State -> MessageObject* is a function that takes as input a state of the system and returns the Message object of the state 

*m* is a constant of type *MessageObject*

*empty* is a constant of type MessageObject denoting an empty message object

*getMessageAudience: MessageObject -> MessageAudience* is a function that takes as input a MessageObject and and returns the audience of the message object

*getPerson: S -> Person* is a function that takes as input a state of the system 

*p* is a constant of type Person

*getType : Person -> pType* is a function that takes as input an element of type Person and returns his type, an element of the set {“Crew”, “Passenger”}

*getLanguage : Person-> pLanguage* is a function that takes as input a Person and returns the language of that person, an element of the set{"English", "Greek", "French" , "Italian"}

*getAssignType : Person -> pAssignType* is a function that takes as input an element of type Person and returns his assignment type, an element of the set{“follow path”, “wait help”}

*getMobilityStatus: Person -> SET_OF_MOBILITY_ISSUES* is a function that takes as input an element of type Person and returns the mobility issue of the person, if any

*SetMessageBody: Person MessageObject MessageBody-> MessageObject* is a function that takes as input a person, a message object and a message body and sets the message body of the message object addressed to that person

*SetMessageFIle: Person MessageObject File-> MessageObject* is a function that takes as input a person, a message object and a message file and includes it in the message object addressed to that person

*SendMessage(p, o)* sends to the Person p the MessageObject  o 

The Passenger Message creation ruleset is triggered after the creation of a message object (event) and defines the message to be sent (action) if the message object is addressed to passengers based on their personalised profile (condition) (and the evacuation phase).

The second rule set of this rule family is defined as;

**Definition 4.2 (RS4.2 - Crew Message creation ruleset):** *The Crew Message creation ruleset is defined as:*
```
ECA(
ON(Message_Object_Composition_Completed)
IF(getMessageObject(S) = m /\ m =/= empty 
/\ m.getMessageAudience() == Crew 
/\ getPerson(S) = p /\ p.getType() == Crew)
THEN DO(SetMessageBody(p, o, message_body) /\ message_body \in String SetMessageFile(p, o, file) /\ file \in SET_OF_FILES /\ SendMessage(p, o)
)
```
In this definition:

*Message_Object_Composition_Completed \in SET_of_Defined_Events*

*getMessageObject: State -> MessageObject* is a function that takes as input a state of the system and returns the message object of that state
m is a constant of type MessageObject

*empty8 is a constant of type MessageObject denoting an empty message object

*getMessageAudience: MessageObject -> messageAudience* is a function that takes as input a MessageObject and and returns the audience of the message object

*getPerson: S -> Person* is a function that takes as input a state of the system and returns the person of the state 

*p* is a constant of type Person

*getType : Person -> pType* is a function that takes as input an element of type Person and returns his type, an element of the set {“Crew”, “Passenger”}

*SetMessageBody: Person MessageObject MessageBody -> MessageObject* is a function that takes as input a person, a message object and a message body and sets the message body of that message object 

*SetMessageFIle: Person MessageObject File -> MessageObject* is a function that takes as input a person, a message object and a file and includes it in the message object 

*SendMessage(p, o)* sends to the Person p the MessageObject  o 

Additionally:
*getEmergencyPost : Person -> Post* is an function that takes as input a person and returns his assigned emergency post

*getEmergencyLocation : State -> Location* is a function that takes as input a state of the system and returns the emergency location of the state

*getEmergencytype : State -> EmergencyType* is a function that takes as input a state of the system and returns the type of the emergency of this state

*getIssueLocation: State -> Location* is a function that takes as input a state of the system and returns the location of the issue of this state (e.g. low performance of mustering process)

*getIncidentLocation : State -> Location* is a function that takes as input a state of the system and returns the location of the incident of this state

*getIncidentType : State -> IncidentType* is a function that takes as input a state of the system and returns the type of the incident of this state

*getAssignedPassenger : State Person -> Person* is a function that takes as input a state of the system and a Crew member that is assigned to help a passenger in need in this state and returns that passenger

The Crew Message creation ruleset essentially is triggered after the creation of a message object (event) and defines the message to be sent (action) if the message object is addressed to the crew based on their emergency posts (condition) (and the evolution of the emergency).

## PaMEAS Evacuation Messaging ECA Rules

RuleSet 1: Evacuation profile rules

Rule 1.1:
```ECA(
ON(Evacuation_Phase_4_Start_event)
IF(getPerson(S) = p and p.Type == PASSENGER and p.Medical_Assistance = none and p.Mobility_Issues = none and p.Pregnancy_data = normal)
THEN DO(Passenger.Assignement_Type == FOLLOW_PATH)
)
```

Rule 1.2:
```
ECA(
ON(Evacuation_Phase_4_Start_event)
IF(getPerson(S) = p and p.Type == PASSENGER and p.Medical_Assistance = equip_required)
THEN DO(Passenger.Assignement_Type == WAIT_HELP)
)
```

Rule 1.3:
```
ECA(
ON(Evacuation_Phase_4_Start_event)
IF(getPerson(S) = p and p.Type == PASSENGER and p.Medical_Assistance = stretcher)
THEN DO(Passenger.Assignement_Type == WAIT_HELP)
)
```

Rule 1.4:
```
ECA(
ON(Evacuation_Phase_4_Start_event)
IF(getPerson(S) = p and p.Type == PASSENGER and p.Medical_Assistance = heavy_doses)
THEN DO(Passenger.Assignement_Type == WAIT_HELP)
)
```

Rule 1.5:
```
ECA(
ON(Evacuation_Phase_4_Start_event)
IF(getPerson(S) = p and p.Type == PASSENGER and p.Mobility_Issues = assisted_gait)
THEN DO(Passenger.Assignement_Type == WAIT_HELP)
)
```

Rule 1.6:
```
ECA(
ON(Evacuation_Phase_4_Start_event)
IF(getPerson(S) = p and p.Type == PASSENGER and p.Mobility_Issues = walking_disability)
THEN DO(Passenger.Assignement_Type == WAIT_HELP)
)
```

Rule 1.7:
```
ECA(
ON(Evacuation_Phase_4_Start_event)
IF(getPerson(S) = p and p.Type == PASSENGER and p.Mobility_Issues = severe_walking_disability)
THEN DO(Passenger.Assignement_Type == WAIT_HELP)
)
```

Rule 1.8:
```
ECA(
ON(Evacuation_Phase_4_Start_event)
IF(getPerson(S) = p and p.Type == PASSENGER and p.Mobility_Issues = unable_to_walk)
THEN DO(Passenger.Assignement_Type == WAIT_HELP)
)
```

Rule 1.9:
```
ECA(
ON(Evacuation_Phase_4_Start_event)
IF(getPerson(S) = p and p.Type == PASSENGER and p.Mobility_Issues = visually_impaired)
THEN DO(Passenger.Assignement_Type == WAIT_HELP)
)
```

Rule 1.10:
```
ECA(
ON(Evacuation_Phase_4_Start_event)
IF(getPerson(S) = p and p.Type == PASSENGER and p.Mobility_Issues = hearing_impaired)
THEN DO(Passenger.Assignement_Type == WAIT_HELP)
)
```

Rule 1.11:
```
ECA(
ON(Evacuation_Phase_4_Start_event)
IF(getPerson(S) = p and p.Type == PASSENGER and p.Mobility_Issues = cognitive_impaired)
THEN DO(Passenger.Assignement_Type == WAIT_HELP)
)
```

Rule 1.12:
```
ECA(
ON(Evacuation_Phase_4_Start_event)
IF(getPerson(S) = p and p.Type == PASSENGER and p.Pregnancy_data = complicated)
THEN DO(Passenger.Assignement_Type == WAIT_HELP)
)
```

RuleSet 2.1: Evacuation path profile rules

Rule 2.1.1:
```
ECA(
ON(Mustering_actions_profile_completed)
IF(getPerson(S)= p and p.Type == PASSENGER and
p.getGeofence(S) = 9G1 and getAssignMSpath(p) == none
and getStatusMSPath(S,[S9-8.1,S8-7.1,7BG2,7BG1]) = free))
THEN DO(AssignMSpath(p,[9G1,S9-8.1,S8-7.1,7BG2,7BG1]))
)
```

Rule 2.1.2:
```
ECA(
ON(Mustering_actions_profile_completed)
IF(getPerson(S)= p and p.Type == PASSENGER and
p.getGeofence(S) = 8G1 and getAssignMSpath(p) == none
and getStatusMSPath(S,[S8-7.1,7BG2,7BG1]) = free))
THEN DO(AssignMSpath(p,[8G1,S8-7.1,7BG2,7BG1]))
)
```

Rule 2.1.3:
```
ECA(
ON(Mustering_actions_profile_completed)
IF(getPerson(S)= p and p.Type == PASSENGER and
p.getGeofence(S) = 8G2 and getAssignMSpath(p) == none
and getStatusMSPath(S,[S8-7.1,7BG2,7BG1]) = free)
THEN DO(AssignMSpath(p,[8G2,S8-7.1,7BG2,7BG1]))
)
```

Rule 2.1.4:
```
ECA(
ON(Mustering_actions_profile_completed)
IF(getPerson(S)= p and p.Type == PASSENGER and
p.getGeofence(S)= 8G3 and getAssignMSpath(p) == none
and getStatusMSPath(S,[S8-7.1,7BG2,7BG1]) = free))
THEN DO(AssignMSpath(p,[8G3,S8-7.1,7BG2,7BG1]))
)
```

Rule 2.1.5:
```
ECA(
ON(Mustering_actions_profile_completed)
IF(getPerson(S)= p and p.Type == PASSENGER and
p.getGeofence(S) = 8G4 and getAssignMSpath(p) == none
and getStatusMSPath(S,[S8-7.2,7BG2,7BG1]) = free))
THEN DO(AssignMSpath(p,[8G4,S8-7.2,7BG2,7BG1]))
)
```

Rule 2.1.6:
```
ECA(
ON(Mustering_actions_profile_completed)
IF(getPerson(S)= p and p.Type == PASSENGER and
p.getGeofence(S) = 8G5 and getAssignMSpath(p) == none
and getStatusMSPath(S,[S8-7.2,7BG2,7BG1]) = free))
THEN DO(AssignMSpath(p,[8G5,S8-7.2,7BG2,7BG1]))
)
```

Rule 2.1.7:
```
ECA(
ON(Mustering_actions_profile_completed)
IF(getPerson(S)= p and p.Type == PASSENGER and
p.getGeofence(S) = 8G6 getAssignMSpath(p) == none
and getStatusMSPath(S,[S8-7.3,7BG1]) = free))
THEN DO(AssignMSpath(p,[8G6,S8-7.3,7BG1]))
)
```

Rule 2.1.8:
```
ECA(
ON(Mustering_actions_profile_completed)
IF(getPerson(S)= p and p.Type == PASSENGER and
p.getGeofence(S) = 8G7 and getAssignMSpath(p) == none
and getStatusMSPath(S,[S8-7.3,7BG1]) = free))
THEN DO(AssignMSpath(p,[8G7,S8-7.3,7BG1]))
)
```

Rule 2.1.9:
```
ECA(
ON(Mustering_actions_profile_completed)
IF(getPerson(S)= p and p.Type == PASSENGER and
p.getGeofence(S) = 8G8 and getAssignMSpath(p) == none
and getStatusMSPath(S,[S8-7.4,7BG1]) = free))
THEN DO(AssignMSpath(p,[8G8,S8-7.4,7BG1]))
)
```

Rule 2.1.10:
```
ECA(
ON(Mustering_actions_profile_completed)
IF(getPerson(S)= p and p.Type == PASSENGER and
p.getGeofence(S) = 8G9 and getAssignMSpath(p) == none
and getStatusMSPath(S,[S8-7.4,7BG1]) = free))
THEN DO(AssignMSpath(p,[8G9,S8-7.4,7BG1]))
)
```

Rule 2.1.11:
```
ECA(
ON(Mustering_actions_profile_completed)
IF(getPerson(S)= p and p.Type == PASSENGER and
p.getGeofence(S) = 8G10 and getAssignMSpath(p) == none
and getStatusMSPath(S,[S8-7.4,7BG1]) = free))
THEN DO(AssignMSpath(p,[8G10,S8-7.4,7BG1]))
)
```

Rule 2.1.12:
```
ECA(
ON(Mustering_actions_profile_completed)
IF(getPerson(S)= p and p.Type == PASSENGER and
p.getGeofence(S) = 7G1 and getAssignMSpath(p) == none
and getStatusMSPath(S,[7G2,7G3,7G4,7BG1]) = free))
THEN DO(AssignMSpath(p,[7G1,7G2,7G3,7G4,7BG1]))
)
```

Rule 2.1.13:
```
ECA(
ON(Mustering_actions_profile_completed)
IF(getPerson(S)= p and p.Type == PASSENGER and
p.getGeofence(S) = 7G2 and getAssignMSpath(p) == none
and getStatusMSPath(S,[7G3,7G4,7BG1]) = free))
THEN DO(AssignMSpath(p,[7G2,7G3,7G4,7BG1]))
)
```

Rule 2.1.14:
```
ECA(
ON(Mustering_actions_profile_completed)
IF(getPerson(S)= p and p.Type == PASSENGER and
p.getGeofence(S) = 7G3 and getAssignMSpath(p) == none
and getStatusMSPath(S,[7G4,7BG1]) = free))
THEN DO(AssignMSpath(p,[7G3,7G4,7BG1]))
)
```

Rule 2.1.15:
```
ECA(
ON(Mustering_actions_profile_completed)
IF(getPerson(S)= p and p.Type == PASSENGER and
p.getGeofence(S) = 7G4 and getAssignMSpath(p) == none
and getStatusMSPath(S,[7BG1]) = free))
THEN DO(AssignMSpath(p,[7G4,7BG1]))
)
```

RuleSet 2.2: Update Evacuation path profile rules

Rule 2.2:
```
ECA(
ON(Evacuation_profile_completed and GeoFence_status_update)
IF(getPerson(S) = p and p.getType() == Passenger and
getStatusMSPath(S,getAssignMSpath(p)) == blocked and
p.getGeofence() =/= p.getAssignMS())
THEN DO (AssignMSpath(p,getAltPath(getAssignMSpath(p),
getBlockedGeofence(S,getAssignMSpath(p)))))
)
```

RuleSet 3: Message object composition rules

Rule 3.1.1:
```
ECA(
ON(Evacuation_Phase_1_Start_event)
IF(Evacuation Process Task == T1.1)
THEN DO(
ComposeMessageObject(t1.1) and
SetMessagetype(1.1,none) and
SetMessageSender(1.1,none) and
SetMessageAudience(1.1,none) and
SetMessageLayout(1.1,none) and
SetMessageChannel(1.1,none) and
SetMessageBody(p, 1.1,empty) and
SetMessageFile(p,1.1, none))
)
```

Rule 3.1.2:
```
ECA(
ON(Evacuation_Phase_1_Start_event)
IF(Evacuation Process Task == T1.2)
THEN DO(
ComposeMessageObject(t1.2) and
SetMessagetype(1.2,notifications) and
SetMessageSender(1.2,EC) and
SetMessageAudience(1.2,crew) and
SetMessageLayout(1.2,[Text,Visual,Voice]) and
SetMessageChannel(1.2,TMS) and
SetMessageBody(p, 1.2,empty) and
SetMessageFile(p,1.2, none))
)
```

Rule 3.1.3:
```
ECA(
ON(Evacuation_Phase_1_Start_event)
IF(Evacuation Process Task == T1.3)
THEN DO(
ComposeMessageObject(t1.3) and
SetMessagetype(1.3,feedback) and
SetMessageSender(1.3,crew) and
SetMessageAudience(1.3,EC) and
SetMessageLayout(1.3,[Text] )and
SetMessageChannel(1.2,TMS) and
SetMessageBody(p, 1.3,empty) and
SetMessageFile(p,1.3, none))
)
```

Rule 3.2.1:
```
ECA(
ON(Evacuation_Phase_1_Start_event)
IF(Evacuation Process Task == T2.1)
THEN DO(
ComposeMessageObject(t2.1) and
SetMessagetype(2.1,communication_session) and
SetMessageSender(2.1,crew) and
SetMessageAudience(2.1,EC) and
SetMessageLayout(2.1,[Text,Voice,Visual,Video]) and
SetMessageChannel(2.1,TMS) and
SetMessageBody(p, 2.1,empty) and
SetMessageFile(p,2.1, none))
)
```

Rule 3.4.1:
```
ECA(
ON(Evacuation_Phase_4_Start_event)
IF(Evacuation Process Task == T4.1)
THEN DO(
ComposeMessageObject(t4.1) and
SetMessagetype(4.1,notifications) and
SetMessageSender(4.1,EC) and
SetMessageAudience(4.1,crew) and
SetMessageLayout(4.1,[Text,Visual]) and
SetMessageChannel(4.1,TMS) and
SetMessageBody(p,4.1,empty) and
SetMessageFile(p,4.1, none))
)
```

Rule 3.4.3:
```
ECA(
ON(Evacuation_Phase_4_Start_event)
IF(Evacuation Process Task == T4.3)
THEN DO(
ComposeMessageObject(t4.3) and
SetMessagetype(4.3,feedback) and
SetMessageSender(4.3,crew) and
SetMessageAudience(4.3,EC) and
SetMessageLayout(4.3,[Text])and
SetMessageChannel(4.1,TMS) and
SetMessageBody(p,4.3,empty) and
SetMessageFile(p,4.3, none))
)
```

Rule 3.5.1:
```
ECA(
ON(Evacuation_Phase_5_Start_event)
IF(Evacuation Process Task == T5.1)
THEN DO(
ComposeMessageObject(t5.1) and
SetMessagetype(5.1,alert) and
SetMessageSender(5.1,PaMEAS) and
SetMessageAudience(5.1,passengers) and
SetMessageLayout(5.1,[Text,Visual,Vibration,Voice]) and
SetMessageChannel(5.1,EMS) and
SetMessageBody(p,5.1,empty) and
SetMessageFile(p,5.1, none))
)
```

Rule 3.6.2:
```
ECA(
ON(Evacuation_Phase_6_Start_event)
IF(Evacuation Process Task == T6.2)
THEN DO(
ComposeMessageObject(t6.2) and
SetMessagetype(6.2,warnings) and
SetMessageSender(6.2,PaMEAS) and
SetMessageAudience(6.2,passengers) and
SetMessageLayout(6.2,[Text,Visual,Vibration,voice]) and
SetMessageChannel(6.2,EMS) and
SetMessageBody(p,6.2,empty) and
SetMessageFile(p,6.2, none))
)
```

Rule 3.6.3:
```
ECA(
ON(Evacuation_Phase_6_Start_event)
IF(Evacuation Process Task == T6.3)
THEN DO(
ComposeMessageObject(t6.3) and
SetMessagetype(6.3,notifications) and
SetMessageSender(6.3,PaMEAS)and
SetMessageAudience(6.3,passengers) and
SetMessageLayout(6.3,[Text,Visual]) and
SetMessageChannel(6.3,EMS) and
SetMessageBody(p, 6.3,empty) and
SetMessageFile(p,6.3,none))
)
```

Rule 3.6.5:
```
ECA(
ON(Evacuation_Phase_6_Start_event)
IF(Evacuation Process Task == T6.5)
THEN DO(
ComposeMessageObject(t6.5) and
SetMessagetype(6.5,notifications) and
SetMessageSender(6.5,PaMEAS) and
SetMessageAudience(6.5,passengers) and
SetMessageLayout(6.5,[Text]) and
SetMessageChannel(6.5,EMS) and
SetMessageBody(p,6.5,empty) and
SetMessageFile(p,6.5,none))
)
```

Rule 3.6.7:
```
ECA(
ON(Evacuation_Phase_6_Start_event)
IF(Evacuation Process Task == T6.7)
THEN DO(
ComposeMessageObject(t6.7) and
SetMessagetype(6.7,notifications) and
SetMessageSender(6.7,EC)and
SetMessageAudience(6.7,crew) and
SetMessageLayout(6.7,[Text,Visual,Voice]) and
SetMessageChannel(6.7,TMS) and
SetMessageBody(p,6.7,empty) and
SetMessageFile(p,6.7,none))
)
```

Rule 3.6.8:
```
ECA(
ON(Evacuation_Phase_6_Start_event)
IF(Evacuation Process Task == T6.8)
THEN DO(
ComposeMessageObject(t6.8) and
SetMessagetype(6.8,warnings) and
SetMessageSender(6.8,EC) and
SetMessageAudience(6.8,crew) and
SetMessageLayout(6.8,[Text,Visual,Voice]) and
SetMessageChannel(6.8,TMS) and
SetMessageBody(p,6.8,empty) and
SetMessageFile(p,6.8,none))
)
```

Rule 3.6.9:
```
ECA(
ON(Evacuation_Phase_6_Start_event)
IF(Evacuation Process Task == T6.9 and
GeoFence_status == updated)
THEN DO(
ComposeMessageObject(t6.9) and
SetMessagetype(6.9,notifications) and
SetMessageSender(6.9,PaMEAS) and
SetMessageAudience(6.9,passengers) and
SetMessageLayout(6.9,[Text,Visual]) and
SetMessageChannel(6.9,EMS) and
SetMessageBody(p,6.9,empty) and
SetMessageFile(p,6.9,none))
)
```

Rule 3.7.2:
```
ECA(
ON(Evacuation_Phase_7_Start_event)
IF(Evacuation Process Task == T7.2)
THEN DO(
ComposeMessageObject(t7.2) and
SetMessagetype(7.2,notifications) and
SetMessageSender(7.2,PaMEAS) and
SetMessageAudience(7.2,passengers) and
SetMessageLayout(7.2,[Text,Visual,Voice]) and
SetMessageChannel(7.2,EMS) and
SetMessageBody(p,7.2,empty) and
SetMessageFile(p,7.2,none))
)
```

Rule 3.8.2:
```
ECA(
ON(Evacuation_Phase_8_Start_event)
IF(Evacuation Process Task == T8.2)
THEN DO(
ComposeMessageObject(t8.2) and
SetMessagetype(8.2,notifications) and
SetMessageSender(8.2,EC) and
SetMessageAudience(8.2,crew) and
SetMessageLayout(8.2,[Text,Visual,Voice]) and
SetMessageChannel(8.2,TMS) and
SetMessageBody(p,8.2,empty) and
SetMessageFile(p,8.2,none))
)
```

Rule 3.8.3:
```
ECA(
ON(Evacuation_Phase_8_Start_event)
IF(Evacuation Process Task == T8.3)
THEN DO(
ComposeMessageObject(t8.3) and
SetMessagetype(8.3,feedback) and
SetMessageSender(8.3,crew) and
SetMessageAudience(8.3,EC) and
SetMessageLayout(8.3,[Text]) and
SetMessageChannel(8.3,TMS) and
SetMessageBody(p,8.3,empty) and
SetMessageFile(p,8.3,none))
)
```

Rule 3.8.4:
```
ECA(
ON(Evacuation_Phase_8_Start_event)
IF(Evacuation Process Task == T8.4)
THEN DO(
ComposeMessageObject(t8.4) and
SetMessagetype(8.4,notifications) and
SetMessageSender(8.4,PaMEAS) and
SetMessageAudience(8.4,passengers) and
SetMessageLayout(8.4,[Text,Visual,Vibration,Voice]) and
SetMessageChannel(8.4,EMS) and
SetMessageBody(p,8.4,empty) and
SetMessageFile(p,8.4,none))
)
```

Rule 3.8.5:
```
ECA(
ON(Evacuation_Phase_8_Start_event)
IF(Evacuation Process Task == T8.5)
THEN DO(
ComposeMessageObject(t8.5) and
SetMessagetype(8.5,communication_session) and
SetMessageSender(8.5,[EC,CrewManagers]) and
SetMessageAudience(8.5,crew) and
SetMessageLayout(8.5,[Text,Voice,Visual,Video]) and
SetMessageChannel(8.5,TMS) and
SetMessageBody(p,8.5,empty) and
SetMessageFile(p,8.5,none))
)
```

RuleSet 4.1: Passenger Message creation rules

Rule 4.1.5.1.1-EN:
```
ECA(
ON(Message_Object_Composition_Completed)
IF(getMessageObject(S) = 5_1 and 5_1.getMessageAudience()
== Passenger and getPerson(S) = p and p.Type == PASSENGER and
p.Language == English and p.getMobilityIssues =/= visually_impaired)
THEN DO(SetMessageBody(p,5.1, “Fire Onboard. Prepare for immediate evacuation.
This is not a drill!!”) and SendMessage(p,5.1))
)
```

Rule 4.1.5.1.2-EN-VI:
```
ECA(
ON(Message_Object_Composition_Completed)
IF(getMessageObject(S) = 5_1 and 5_1.getMessageAudience()
== Passenger and getPerson(S) = p and p.Type == PASSENGER and
p.Language == English and p.getMobilityIssues == visually_impaired)
THEN DO(SetMessageBody(p,5.1, “Fire Onboard. Prepare for immediate evacuation.
This is not a drill!!”) and SetMessageFile(p,5.1,textToSpeech_recording_en)
and SendMessage(p,5.1))
)
```

Rule 4.1.6.2.1-EN:
```
ECA(
ON(Message_Object_Composition_Completed)
IF(getMessageObject(S) = 6_2 and 6_2.getMessageAudience()
== Passenger and getPerson(S) = p and p.Type == PASSENGER and
p_Assign_Type == FOLLOW_PATH and p.Language == English)
THEN DO(SetMessageBody(p, 6.2, “Put on your life jacket, remain calm and
wait for instructions. Lifejackets are stored in your cabins under your bed
and at the master stations.”) and
SendMessage(p,6.2))
)
```

Rule 4.1.6.3.1-EN:
```
ECA(
ON(Message_Object_Composition_Completed)
IF(getMessageObject(S) = 6_3 and 6_3.getMessageAudience() == Passenger and
getPerson(S) = p and p.Type == PASSENGER and p_Assign_Type == FOLLOW_PATH
and p.Language == English)
THEN DO(SetMessageBody(p, 6.3, “Access to Master Station ‘AssignedMasterStation’ is
via the following path: “PathDescription”) and
SetMessageFile(p,6.3,pathImage) and SendMessage(p,6.3))
)
```

Rule 4.1.6.5.1-EN:
```
ECA(
ON(Message_Object_Composition_Completed)
IF(getMessageObject(S) = 6_5 and 6_5.getMessageAudience() == Passenger and
getPerson(S) = p and p.Type == PASSENGER and p_Assign_Type == WAIT_HELP
and p.Language == English and p.getMobilityIssues =/= visually_impaired)
THEN DO(SetMessageBody(p,6.5,“Please remain in your location. A crew member
is on the way to escort you to the master station and will arrive to you really
shortly.”) and SendMessage(p,6.5))
)
```

Rule 4.1.6.5.2-EN:
```
ECA(
ON(Message_Object_Composition_Completed)
IF(getMessageObject(S) = 6_5 and 6_5.getMessageAudience() == Passenger and
getPerson(S) = p and p.Type == PASSENGER and p_Assign_Type == WAIT_HELP and
p.Language == English and p.getMobilityIssues == visually_impaired)
THEN DO(SetMessageBody(p,6.5,“Please remain in your location. A crew member
is on the way to escort you to the master station and will arrive to you really
shortly.”) and SetMessageFile(p,6.5,textToSpeech_recording_en)
and SendMessage(p,6.5))
)
```

Rule 4.1.6.9.1-EN:
```
ECA(
ON(Message_Object_Composition_Completed)
IF(getMessageObject(S) == 6_9 and 6_9.getMessageAudience() == Passenger and
getPerson(S) = p and p.Type == PASSENGER and p_AssignType == FOLLOW_PATH and
p.Language == English)
THEN DO(SetMessageBody(p,6.9,“’BlockedGeofence’ has been blocked. Follow the
alternative path below: ‘PathDescription’.”) and SetMessageFile(p,6.9,PathImage)
and SendMessage(p,6.9))
)
```

Rule 4.1.6.7.2-EN:
```
ECA(
ON(Message_Object_Composition_Completed)
IF(getMessageObject(S) == 7_2 and 7_2.getMessageAudience() == Passenger and
getPerson(S) = p and p.Type == PASSENGER and p_AssignType == WAIT_HELP and
p.Language == English)
THEN DO(SetMessageBody(p,7.2,“Go now to the embarkation station.
Keep your lifejacket on at all times.”)
and SendMessage(p,7.2))
)
```

Rule 4.1.8.4.1-EN:
```
ECA(
ON(Message_Object_Composition_Completed)
IF(getMessageObject(S) = 8_4 and 8_4.getMessageAudience() == Passenger and
getPerson(S) = p and p.Type == PASSENGER and p.Language == English and
p.getMobilityIssues =/= visually_impaired)
THEN DO(SetMessageBody(p,8.4,“Please remain in your location. Assistance is on the
way and should arrive to you really shortly.”) and SendMessage(p,8.4))
)
```

RuleSet 4.2: Crew Message creation rules

Rule 4.2.1.2:
```
ECA(
ON(Message_Object_Composition_Completed)
IF(getMessageObject(S) == 1_2 and 1_2.getMessageAudience() == crew and
getPerson(S) = p and p.Type == crew)
THEN DO(SetMessageBody(p,1.2,”Proceed to the hazard area:
‘getEmergencyLocation’ and provide confirmation!!”) and
SetMessageFile(p,1.2,PathImage) and SendMessage(p,1.2))
)
```

Rule 4.2.4.1:
```
ECA(
ON(Message_Object_Composition_Completed)
IF(getMessageObject(S) == 4_1 and 4_1.getMessageAudience() == crew and
getPerson(S) = p and p.Type == crew)
THEN DO(SetMessageBody(p,4.1,”Assume your emergency post: ‘EmergencyPost’!”)
and SendMessage(p,4.1))
)
```

Rule 4.2.6.7:
```
ECA(
ON(Message_Object_Composition_Completed)
IF(getMessageObject(S) == 6_7 and 6_7.getMessageAudience() == crew and
getPerson(S) = p and p.Type == crew and == passenger_assistance_units and
p.AssignedPassenger = pi and getPInNeed(S) = pi)
THEN DO(SetMessageBody(p,6.7,”Proceed to ‘IncidentLocation’. Passenger speaking
’Passenger Language’, with [‘MobilityIssues’, ‘PregnancyStatus’, ‘MedicalAssistance’],
needs assistance to evacuate.”) and SetMessageFile(p,6.7,PathImage)
and SendMessage(p,6.7))
)
```

Rule 4.2.6.9:
```
ECA(
ON(Message_Object_Composition_Completed)
IF(getMessageObject(S) == 6_9 and 6_9.getMessageAudience() == Crew
and
getPerson(S) = p and p.Type == crew)
THEN DO(SetMessageBody(p,6.9,“’BlockedGeofence’ has been blocked.
Follow the alternative path below: ‘PathDescription’.") and
SetMessageFile(p,6.9,PathImage) and SendMessage(p,6.9))
)
```

Rule 4.2.8.2:
```
ECA(
ON(Message_Object_Composition_Completed)
IF(getMessageObject(S) == 8_2 and 8_2.getMessageAudience() == crew and
getPerson(S) = p and p.Type == crew)
THEN DO(SetMessageBody(p,8.2,”Proceed to ‘IncidentLocation’.
Passenger needs help! Passenger speaking ’Passenger Language’ is ’Incident Type’.”)
and SetMessageFile(p,8.2,PathImage) and SendMessage(p,8.2))
)
```

PaMEAS Evacuation Messaging Policy is intended to supplement the Ship’s emergency communications strategy in the context of the PALAEMON project. 
This policy is dedicated to the TMS-MCPTT Tactilon-Agnet Service, the 5G IMS services and the EMS-Evacuation Management Service managed by the PaMEAS-A system.
This policy is intended for emergency use.
