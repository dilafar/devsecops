### falco doc
    https://falco.org/docs/
    
### install falco (linux)
    https://falco.org/docs/getting-started/falco-linux-quickstart/

## add custom falco rules
### supported fields 
    https://falco.org/docs/reference/rules/supported-fields/

### falco-security rules
    https://github.com/falcosecurity/rules/blob/main/rules/falco_rules.yaml

### vim /etc/falco/falco_rules.local.yaml  and add the below rules
    - macro: custom_macro
      condition: evt.type = execve and container.id != host

    - list: blacklist_binaries
      items: [cat, grep, date]

    - rule: The program "cat" is run in a container
      desc: an event will trigger every time you run cat in a container
      condition: custom_macro and proc.name in (blacklist_binaries)
      output: "cat was run inside a container (user=%user.name container=%container.name image=%container.image proc=%proc.cmdline)"
      priority: INFO 

### run falco
    falco

### test falco rules
    kubectl get pods
    kubectl exec -it nginx -- bash
    cd /etc
    cat hosts

### Example Use Case - (capture log for 25 secods and store it in /tmp/log.txt)
### Format as follows 
    time uid process-name

### solution
    - macro: custom_macro
    condition: evt.type = execve and container.id != host

    - list: blacklist_binaries
      items: [cat, grep, date]

    - rule: The program "cat" is run in a container
      desc: an event will trigger every time you run cat in a container
      condition: custom_macro and proc.name in (blacklist_binaries)
      output: demo %evt.time %user.uid %proc.name
      priority: INFO  
### create a file
        touch logs.txt
### run and paste the demo output in logs.txt
        timeout 25s falco | grep demo
### filter
        cat logs.txt | awk '{print $4 " " $5 " " $6}' > /tmp/log.txt
        cat /tmp/log.txt

