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


PaMEAS Evacuation Messaging Policy is intended to supplement the Ship’s emergency communications strategy in the context of the PALAEMON project. 
This policy is dedicated to the TMS-MCPTT Tactilon-Agnet Service, the 5G IMS services and the EMS-Evacuation Management Service managed by the PaMEAS-A system.
This policy is intended for emergency use.


