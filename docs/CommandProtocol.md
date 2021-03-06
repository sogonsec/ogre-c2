# Stuff C2 Commands Need To Do or Handle

The list below is a brainstorm of ideas and things that would be handy. All of these commands are secret and C2 operational stuff is hidden/clandestine from normal activity (although transferring a ton of data or using services, and agents, in an non-sneaky way could raise alarms if it is being monitored... like a ton of DNS requests at once that make no sense or appear odd).

I've never really used a C2 before, so this is mostly what I'd like to do if I had a compromised machine hooked up to my C2 server, that I could then make use of in a way that would be useful, especially if it would be a PITA to connect back to and do things (like say running a single command is multiple steps and having to parse through garbage). No idea now practical, but why not give it a shot. The bulk of the hard stuff will be on the agents.

Note: all network communications should be encrypted in transit tunnels and data, if possible, unless normal behavior sneakiness is the priority.

I may want to consider making the protocol binary instead of ascii. It would use less bytes and have less strings in the binaries and streams. As long as the protocol is easy for humans to figure out when coding (documentation) then it shouldn't be that big a deal. I'm writing it so I get the luxury of doing what I want :) Probably want a decoder/encoder from ascii to binary anyways for the compression/encryption/obfuscation stuff anyways, so bake it in... probably a few pages of defines or an array of bytes with the ascii in comments for humans... should be able to fit a command in a byte or three, and then payload (where applicable after). 

All agent commands are queued, even if there's only one.

More thought will need to be put into a queue, since the queued commands also may require data back (even just a status message) and it needs to be tracked with the queued commands. Try to not get too carried away with a queue, because all data storage should only exist in RAM to not have evidence on-disk? 

- playbook for doing actions from the agent to the server (such as "normal" email sending: resolve domain, check spf, check DKIM, check MX, send SMTP email) to appear clandestine and not ring any blue team bells (casually... of course good blue teams will know which DNS and SMTP servers you're supposed to use in corp networks, but got to at least try)
    - words: playbook get set neveruse ignore execute
    - target: server and agent
- domain names for server
    - words: domain get set update change rotate random order swiss
    - target: server and agent
- authenticate and get a token (that allows a human/bot to do things with the server that is abnormal, otherwise it is simply a server running services that may or may not work well)
    - words: auth authenticate token session
    - target: server
- report on services and status
    - words: report service services stat status
    - target: server
- display authenticated history
    - words: display auth authenticated hist history
    - target: server
- report on current agents/compromised machines (with an estimate of how reliable the agents/compromised machines are still owned and operational)
    - words: report agents machines operational owned alive current
    - target: server
- run command on an agent
    - words: command cmd run
    - target: agent
- read/write files via an agent
    - words: files file read write in out save download upload
    - target: agent
- privesc via agent
    - words: privup privesc get system admin root sudo super su
    - target: agent
- persist via agent
    - words: persist infest persistence burrow
    - target: agent
- remove all trace from compromised machine via agent
    - words: wipe cleanup remove trace sanitize
    - target: agent
- invalidate all tokens 
    - words: invalidate all token tokens sessions session
    - target: server
- kill all current agent connections
    - words: disconnect kill all client net network stop dark
    - target: server and agent
- get an interactive shell via an agent (even if emulated)
    - words: get shell terminal interactive repl
    - target: server and agent
- report on installed compromised system OS, patches, packages/apps install, users and groups, network info, uptime, system hardware stats (ram, cpu, disks, network cards, webcams, etc) via agent
    - words: report system info all os patches apps users groups network uptime hardware
    - target: agent
- allow other users to the server to authenticate (key pair??)
    - words: grant add permit admin access user key
    - targets: server
- is the compromised machine on the Internet directly (via agent)
    - words: internet ip bound
    - target: agent
- compromised machine firewall rules (via agent)
    - words: firewall fw rules 
    - target: agent
- security protections enabled on compromised machine (via agent)
    - words: security sec prot protections enabled en
    - target: agent
- winpeas/linpeas/linenum.sh output or compatible checks
    - words: enum enumerate local locally 
    - target: agent
- agent operational modes for detection (super sneaky or super loud/who cares, etc)
    - words: oper operate operational mode 
    - target: agent
- shells (reverse and bound)
    - words: shell sh reverse bind bound rev
    - target: server (reverse) and agent (bind)
- agent check in with server every so often for commands to run (guess a queue will be required). This is mainly for compromised hosts that may not be directly routable or addressable, like if it is behind a NAT or FW blocks inbound but not outbound, etc. Probably need more thought into a queue because a single queue item could take multiple protocol requests to get the entire thing (like say if you were depositing a binary file); *TLDR: a queue*
    - words: queue check get next id 
    - target: server and agent
- agent heartbeat to let the server know the agent is still operational (configurable if enabled and needs to have non-static timing/behavior)
    - words: phonehome heartbeat checkin ping newphone whodis
    - target: agent
    


