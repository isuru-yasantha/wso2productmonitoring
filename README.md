# wso2productmonitoring
This repo contains monitoring and logging implementation stacks, helm chart for WSO2 products. This is a sample of kubernetes pod definiton for WSO2 IS server and it showcases how to configure fluent bit and prometheus java agent to collect logs and expose the metrics. You can follow the sample configuration for wso2 is and implement the same in any of wso2 product. You need to add below configuration to wso2server.sh in order to expose the metrics. 

    -javaagent:/home/wso2carbon/prometheus/jmx_prometheus_javaagent-0.12.0.jar=1234:/home/wso2carbon/prometheus/prometheus-jmx-config.yaml 
    
 Jar file can be downloaded at https://repo1.maven.org/maven2/io/prometheus/jmx/jmx_prometheus_javaagent/0.12.0/jmx_prometheus_javaagent-0.12.0.jar and configuration file as below,   
     
 prometheus-jmx-config.yaml  
---
startDelaySeconds: 30
ssl: false
lowercaseOutputName: true
username: [wso2-admin-username]
password: [wso2-admin-user-password]

You need to copy these files to wso2 product container when you build the product image.

Use following commands to install helm chart of monitoring stack. You have to pass tls certificate using kubernetes secret(cert in this helm chart) in order to enable HTTPS for the domain of grafana.x.com or kibana.x.com.

helm install monitoring-stack monitoring-stack -n [namespace]
