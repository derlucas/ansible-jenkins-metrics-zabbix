# Monitoring Jenkins using Metrics Plugin and Zabbix

## This solution is composed by three parts
 1. Jenkins' [Metrics Plugin](https://wiki.jenkins-ci.org/display/JENKINS/Metrics+Plugin)
 2. A python (2) script, which gets metrics from above plugin and transform it in a readable Zabbix item.
 3. A Zabbix Agentd config file which runs the above script and sends result to  Zabbix server

## Install
Install the Metrics Jenkins plugin, create a API Key (Jenkins->Configure->Metrics)
Install this ansible role, configure the variables "zabbix_jenkins_url" and "zabbix_jenkins_key".

---

## Appendix
### How this python script works
It simply uses Jenkins' [Metrics Plugin](https://wiki.jenkins-ci.org/display/JENKINS/Metrics+Plugin)’s API to get a Json containing metrics and transforms it in a more readable file to Zabbix.

However you can also make use of it without a Zabbix, like shown bellow:

```
python jenkins-metrics.py
```

This will return all the metrics at once. If you want to get just one of the metrics, use a full path to a metric item. For example, to get this metric

```
{
  "gauges" : {
    "jenkins.executor.count.value" : {
      "value" : 52
    },
...
```
 
You can type:

```
python jenkins-metrics.py gauges.jenkins.executor.count.value.value
```
