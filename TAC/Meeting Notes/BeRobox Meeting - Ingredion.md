###### 2025-06-06
---
https://docs.google.com/document/d/1jjXaDWglO8W0aKsjfOt7Cx7YOfQjgFbQ-xdxzhuKy1s/edit?tab=t.0

Meeting with Jae & Alex
### Intro
Filtering down...
	compressed air doesn't work - need to use vac pump
	have to use industrial FANUC
no need to change palletizing patterns, so no value there

### HMI
issue with having two HMIs provided
how is HMI being published? Yes, it is https webpage (?)
We could collaborate with BeRobox dev team to share tools and integrations
## Questions:
1. Can we change the layout of the arm with the standard COTS PALTZ?
   
	1. What customizability is there?
	   
	2. Stackit Package vs Modifying Off the Shelf?
	   
	3. Can the HMI be installed elsewhere and ‘remote’ over to the arm?
	   yes, moveable, HDMI cable, etc.
	   
	4. Arm brands supported by Stackit?
	   Doosan and Func Collaborative
	   In progress on 45kg (July) and 50 kg robot
	   Palle - Compatible with?
	   
2. Can the arm reach behind it? What is the allowed range of motion for the arm?
   If safety system is set up, then yes we have capability
   We have to do risk assessment ourselves
   
3. Comms with PLC? State Machine?
   yes, digital signals IO
   Micrologics, only 1 or 2
   compact logics?
   mostly send out pallet completed signals, etc.
   We can re-wire their sensors or grab sensor info from system
   Micrologics is totally replaceable with Beckhoff, it talks digital IO
   
4. Software Dev Documentation?
   Will interface with dry contacts
   API from more complex PC? No, not available
   
5. EOAT recommendations?
   Using Shmaltz
   
	1. Concerns around vacuum in a powdered material facility?
	   explosive ratings
	   
6. Can we weigh with Paltz?
   needs stable read for 1-2 sec
   recommend putting weigh system under pallet, but can't do that
   
7. Flow perpendicular to palletizing?
   
8. Considerations for Slip Sheet module
   might be able to do this w/ vac pump
   need to double check w/ Berobox tech team to make sure we can use vac pump for slip sheets
   possibly adjust vac pump pressure w/ VFD from TAC's side
   Alex feels this should be a solvable problem
   
## Layout
Picking from the side? Pickup location is force to be in front of robot, but that can be recalibrated?

### Closing Questions:
1. What issues/problems do you foresee?
2. Suggestions/guidance?

## Action Items
Obtain whatever documentation about Micrologics software

# Alex about industry
now that palletizers are in industry, people have ideas on how they work
You get product, them begin to have ideas on "oh yeah but it should also be able to do this" - you get feedback on expanding features
TAC happy to 'hand-off' that extra little feature work to BeRobox R&D team
TAC gets a cut every time BeRobox sells one of these extra little features.