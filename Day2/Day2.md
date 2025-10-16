#### Test Rules and First queries

# create test user

net user demoUser P@ssw0rd! /add
--Related query: agent.name:"Windows10_bob" AND data.win.system.eventID:4720

# add to Administrators

net localgroup Administrators demoUser /add  
-- Related query: agent.name:"Windows10_bob" and (data.win.system.eventID:4720 or data.win.system.eventID:4728 or data.win.system.eventID:4672)

# delete test user (remove activity)

net user demoUser /delete
-- Related query: agent.name:"Windows10_bob" AND data.win.system.eventID:4726

# create a scheduled task (persistence demo)

schtasks /create /sc once /tn "DemoTask" /tr "C:\Windows\System32\calc.exe" /st 18:30
-- Related query: agent.name:"Windows10_bob" AND data.win.system.eventID:7

# remove antivirus (evasion demo)

Set-MpPreference -DisableRealtimeMonitoring $true
-- Related query: agent.name:"Windows10_bob" AND data.win.system.eventID: 5001
