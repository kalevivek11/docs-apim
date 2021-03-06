# Alert Types

WSO2 APIM currently supports the following alert types.

-   Abnormal response time
-   Abnormal backend time
-   Abnormal request counts
-   Abnormal resource access pattern
-   Unseen source IP address
-   Frequent tier limit hitting (tier crossing)
-   Availability of APIs (API health monitoring)

### Abnormal response time

|                       |                                                                                                                                                                                                              |
|-----------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Reason for triggering | If there is a sudden increase in the response time of a specific API resource.                                                                                                                               |
| Indication            | Slow WSO2 API Manager runtime, or slow backend.                                                                                                                                                              |
| Description           | This alert gets triggered if the response time of a particular API is higher than the configured value. These alerts could be treated as an indication of a slow WSO2 API Manager runtime or a slow backend. |

### Abnormal backend time

|                       |                                                                                                                                                                                        |
|-----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Reason for triggering | If there is a sudden increase in the backend time corresponding to a particular API resource.                                                                                          |
| Indication            | Slow backend                                                                                                                                                                           |
| Description           | This alert gets triggered if the backend time corresponding to a particular API is higher than the configured value. These alerts could be treated as an indication of a slow backend. |

### Abnormal request counts

|                       |                                                                                                                                                                                                                                                                                                                |
|-----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Reason for triggering | If there is a sudden spike or a drop in the request count within a period of one minute by default for a particular API resource.                                                                                                                                                                              |
| Indication            | These alerts could be treated as an indication of a possible high traffic, suspicious activity, possible malfunction of the client application, etc.                                                                                                                                                           |
| Description           | This alert is triggered if there is a sudden spike in the request count within a period of one minute by default for a particular API for an application. These alerts could be treated as an indication of a possible high traffic, suspicious activity, possible malfunction of the client application, etc. |

### Abnormal resource access pattern

|                       |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|-----------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Reason for triggering | If there is a change in the resource access pattern of a user who uses a particular application.                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| Indication            | These alerts could be treated as an indication of a suspicious activity made by a user over your application.                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| Description           | A Markov Chain model is built for each application to learn its resource access pattern. For the purpose of learning the resource access patterns, no alerts are sent during the first 500 (default) requests. After learning the normal pattern of a specific application, WSO2 Analytics performs a real time check on a transition done by a specific user, and sends and alert if it is identified as an abnormal transition. For a transition to be considered valid, it has to occur within 60 minutes by default, and it should be by the same user. <br /> <br /> ![Abnormal resource access](../../../assets/img/learn/alerts-abnormal-resource-access.png) <br /><br /> The above diagram depicts an example where a Markov Chain model is created during the learning curve of the system. Two states are recorded against Application A and the arrows show the directions of the transitions. Each arrow carries a probability value that stands for the probability of a specific transition taking place. Assume that the following two consecutive events are received by the application from user john@abc.com. <br /><br /> 1. `DELETE /API1/number/1` <br /> 2. `DELETE /API1/number/3` <br /><br /> The above transition has happened from the `DELETE /API1/number/{x}` state to itself. According to the Markov chain model learnt by the system, the probability of this transition occurring is very low. Therefore, an alert is sent. <br /><br /> This alert is triggered if there is a change in the resource access pattern of a user of a particular application. These alerts could be treated as an indication of a suspicious activity made by a user over your application.                                                                                                                                                                                                                                                                                                                             |

### Unseen source IP address

|                       |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
|-----------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Reason for Triggering | If there is either a change in the request source IP for a specific API of an application, or if the request if from an IP used before 30 days (default).                                                                                                                                                                                                                                                                                                                                                                                                               |
| Indication            | These alerts could be treated as an indication of a suspicious activity made by a user over an application.                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| Description           | ![Unseen source IP alert](../../../assets/img/learn/alerts-unseen-source-ip.png) <br /><br /> This alert is triggered if there is either a change in the request source IP for a particular application by a user or if the request is from an IP used before a time period of 30 days (default). The first 100 requests by a user are used only for learning purposes by default and therefore, no alerts are sent during that time. However, the learning would continue even after the first 100 requests by a user. This means, even if you receive continuous requests from the newly detected `IP2` IP, you are alerted only once.  |

### Frequent tier limit hitting (tier crossing)

|                       |                                                                                                                                                                                                                      |
|-----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Reason for Triggering | This alert is triggered in the following scenarios. <ul><li> If a particular application is throttled for reaching a subscribed tier limit more than the specified number of times during a defined period (10 times within an hour by default).</li><li>If a particular user of an application is throttled for reaching a subscribed tier limit of a specific API more than the specified number of times during a defined period (10 times within an hour by default).</li></ul>![Tier crossing alert](../../../assets/img/learn/alerts-frequent-tier-limit-hitting.png)                                                                                                                                                                              |
| Indication            | These alerts indicate that you need to subscribe to a higher tier.                                                                                                                                                   |

### Availability of APIs (API health monitoring)

These alerts are triggered for the reasons specified in the tables below.

|                       |                                                                                                                                                                               |
|-----------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Reason for Triggering | The response time of an API is greater than the configured value specified for the same. This should occur continuously for a specified number of times (5 times by default). |
| Indication            | The response time is too high.                                                                                                                                                |

|                       |                                                                                                                                                                                                |
|-----------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Reason for Triggering | The response status code is greater than or equal to 500, but less than 600. This should occur continuously for a specified number of times (5 times by default) in order to trigger an alert. |
| Indication            | A server side error has occurred.                                                                                                                                                              |

!!! info
     For more information on API status changing over availability of APIs, see [Viewing Availability Of APIs](../../../../learn/analytics/analyzing-apim-statistics-with-batch-analytics/viewing-api-statistics/#availability-of-apis/).



