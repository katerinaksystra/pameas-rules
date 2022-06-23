PaMEAS Evacuation Messaging ECA Rules

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
``

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
``

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


