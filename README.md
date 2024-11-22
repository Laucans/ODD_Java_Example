# Provide an example of ODD (Observability Driven Development) using java

# First words

The following information are my personal interpretation. People can disagree about some definition. 
The article have to be read has a guidance instead of absolute truth.

## What is _DD

"Something-Driven Development" emerged with practices like TDD (Test-Driven Development) and gained popularity 
through advocates such as Kent Beck.

At its core, "Driven Development" emphasizes the idea that a specific focus or mains acts as the guiding force 
throughout the software development process. By adhering to this guiding principle, teams align their decisions, priorities, and methodologies around a central objective, whether it be tests, behaviors, or recently observability.

### TDD Test driven development

Personally, I distinguish TDD and BDD based on the scope of the tests being written.
TDD focuses primarily on unit tests, targeting specific pieces of business logic.

This approach helps identify dependencies and encourages designing code in a testable and modular way, 
with business logic isolated in so-called pure functions.

Let's take an example: you want to compare temperatures between two cities.
Temperature data is provided by an external service accessible via HTTP.

Our first reflex might be to write something like this:
```Java
    boolean isFirstCityWarmer(String city1, String city2) throws Exception {
        // fetchTemperature make HTTP calls
        double temp1 = fetchTemperature(client, city1);
        double temp2 = fetchTemperature(client, city2);
        
        return temp1 > temp2;
    }
```
Here, you would need to mock your HTTP calls directly within the code, or use a stub, which tightly couples the test logic with external dependencies.
Let's work on a good design now :
```Java
    boolean isFirstCityWarmer(String city1, String city2) throws Exception {
        double temp1 = fetchTemperature(client, city1);
        double temp2 = fetchTemperature(client, city2);
        
        return isFirstCityWarmer(temp1, temp2);
    }
    
    boolean isFirstCityWarmer(double temp1, double temp2) {
        return temp1 > temp2;
    }
```
In the second example, the business logic (comparison of temperatures) is isolated in a pure function, making it easy to test independently of the HTTP calls.

TDD should help you identify what constitutes your business logic and ensure that your tests focus on it directly, without being affected by external dependencies.

### BDD Behaviour driven development

Some people say that BDD is an extension of TDD where natural language is used, and that’s true! 
But with the previous definition of TDD, BDD is much more. 
It introduces a new kind of guidance: no longer focusing on individual functions, 
but on features; no longer thinking purely in terms of code, but in terms of system design.  

With BDD, we consider aspects like naming conventions for our data, the definition of interfaces, and much more. 
This approach shifts the focus from unit tests to integration and components tests, emphasizing the interaction 
between components rather than their isolation.  

### ODD Observability driven development

ODD, the latest approach, talks about observability.

> Wait, how can observability drive development? No way!

Well, you’re partially right.  
"Driven development" can sound a bit like marketing. But in reality, observability drives your product, and ultimately, your development. How?

By drawing inspiration from the Lean methodology, which can be roughly summarized by:

> "You must adapt your project by understanding your customers' behaviors. To do this, you need deliver often with small release and measure evolution of what they do and how they interact with your product, using predefined indicators."

Apologies to the Lean community for this oversimplification!

The goal is to prioritize observability early on, ensuring you have all the necessary insights to understand both the current state of your application and how it is being used.
This allows you to make informed decisions about your roadmap and priorities.


## ODD, for and against 

| For                                                                       | But                                                                        |
|---------------------------------------------------------------------------|----------------------------------------------------------------------------|
| Understand customer behaviour                                             | Only useful if the application is used by someone                          |
| Help identify and fix issues faster                                       | Might encourage skipping proper testing phases in favor of reactive fixes. |
| Provides insights to optimize application performance                     | Limited depending experience of the team.                                  |
| Supports better scaling and reliability strategies                        | Needs continuous tuning as the application evolves.                        |
| Improves collaboration between teams by creating a shared source of truth | Relies on teams being trained in using and understanding the data.         |


| Against                                                                                   | But                                                                          |
|-------------------------------------------------------------------------------------------|------------------------------------------------------------------------------|
| Need a large infra which have to be maintained                                            | You can use costly SaaS monitoring system like Datadog.                      |
| Data collection take space and have to be Conciliating with regulation ( like RGPD in EU) |                                                                              |
| Lean approach is necessary to unlock the true power of ODD                                | Lean practices are generally beneficial.                                     |
| You have to build your app, and your observability at the same time                       | Planning observability alongside development ensures a smoother integration. |
| Can lead to over-engineering, focusing too much on metrics and dashboards                 | Staying focused on meaningful KPIs helps avoid this trap.                    |
| Adds additional cost to the project (tools, infrastructure, and expertise)                | Many open-source tools (e.g., Prometheus, Grafana) can reduce expenses.      |

As an indication I suggest using it in:  
1. The context of a startup innovating and seeking to validate its hypotheses while being ready to pivot if necessary.
2. A critical project requiring robust observability to ensure reliability and performance.
3. The creation or enhancement of a complex information system with multiple interconnected services.

And avoid in case of : 
1. Small-scale projects or MVPs without immediate scalability needs.
2. Environments with insufficient budget. ( Can be the case of many startup... you have to measure for and against depending on your context)
3. Projects with low criticality


## Bad opinion, ODD is for Devops

# Focus on ODD

### Observability definitions

## Metrics

## Logs

## Traces

### Observability concepts

### Observability tools



