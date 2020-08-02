# doubledoors.sk
Source code

#!
#!  Please do not edit this skript unless you know what you are doing!
#!
#!  if you encounter any issues please reach out and let me know and
#!   I will do my best to fix them!
#!
#!  This skript was coded by VistoGamingYT
#!    If used or edited give credit where credit is due please and
#!      thank you :)
#!

options:
  perm: dd.core
  perm.message: &cYou dont have permisson to do this!
version: 1.0 #! Do not change this!

on place:
  if event-block is wooden door:
    loop blocks in radius 1 around event-block:
      if loop-block is door:
        add location of event-block to {double.door::*}
        add location of loop-block to {double.door::*}
        set {opened.%location of event-block%} to false

on right click:
  if {opened.%location of event-block%} is true:
    if event-block is wooden door:
      loop blocks in radius 1 around event-block:
        if {double.door::*} contains location of event-block:
          if {double.door::*} contains location of loop-block:
            cancel event
            deactivate event-block
            deactivate loop-block
            set {opened.%location of event-block%} to false
  else:
    if {opened.%location of event-block%} is false:
      if event-block is wooden door:
        loop blocks in radius 1 around event-block:
          if {double.door::*} contains location of loop-block:
            if {double.door::*} contains location of event-block:
              cancel event
              activate event-block
              activate loop-block
              set {opened.%location of event-block%} to true
#!
#!
#!  Be Advised the command below should only be ran as a last resort to fix
#!  any issues u may be having as it clears the location of all double doors
#!  and will require them to be replaced!
#!
#!
command /clear:
  permission: {@perm}
  permission message: {@perm.message}
  trigger:
    delete {double.door::*}
