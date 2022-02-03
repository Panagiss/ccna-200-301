# **Traditional IT Services Deployment Models**
- Traditional deployment models for IT services available before Cloud:
  - On Premises solutions
  - Colocation or ‘Colo’ services

## **On Premises Solutions Characteristics**
- All equipment is located in your building
- All equipment is owned by you
- There are clear lines of demarcation – everything in the building is your responsibility, the connections between offices are your network service provider’s responsibility
- Equipment is CapEx
- New equipment will typically take over a week to deploy
- Equipment requires technology refreshes
- You need to consider redundancy

## **Colocation Facilities**
- A colocation centre or “colo", is a data center location where the owner of the facility rents out space to external customers
- The facility owner provides power, cooling, and physical security for their customer’s server, storage, and networking equipment
- Your user desktops will still be in your offices


# **Defining Cloud Computing**
- Beginners tend to describe Cloud Computing as ‘IT services which are located “somewhere else”’
- But colo facilities are off premises, and they’re not cloud
- And private cloud deployments are often on premises
- So we need a better definition…





The National Institute of Standards and Technology provided the

industry standard definition of Cloud Computing in 2011:

*‘Cloud computing is a model for enabling ubiquitous, convenient, on-*

*demand network access to a shared pool of configurable computing*

*resources (e.g., networks, servers, storage, applications, and services)*

*that can be rapidly provisioned and released with minimal*

*management effort or service provider interaction.’*


## **Cloud Characteristics**
- On-demand self service
- Rapid elasticity
- Broad network access
- Resource pooling
- Measured service

# **Virtualization**
- Virtualization is one of the main enablers of Cloud Computing
- It allows for resource pooling where multiple customers share the underlying hardware
- Virtualization has been around a lot longer than Cloud Computing though
- This lecture focuses on server virtualization because it was the first type available, but the same principles can be applied to virtualize network infrastructure equipment

![](images/Cloud/Aspose.Words.e650799a-1137-4e9d-91c4-04daf8c20ba7.001.png)

![](images/Cloud/Aspose.Words.e650799a-1137-4e9d-91c4-04daf8c20ba7.002.png)

![](images/Cloud/Aspose.Words.e650799a-1137-4e9d-91c4-04daf8c20ba7.003.png)

![](images/Cloud/Aspose.Words.e650799a-1137-4e9d-91c4-04daf8c20ba7.004.png)

![](images/Cloud/Aspose.Words.e650799a-1137-4e9d-91c4-04daf8c20ba7.005.png)

## **Type 1 vs Type 2 Hypervisor**
![](images/Cloud/Aspose.Words.e650799a-1137-4e9d-91c4-04daf8c20ba7.006.png)


# **Virtualization on Network Devices**
![](images/Cloud/Aspose.Words.e650799a-1137-4e9d-91c4-04daf8c20ba7.007.png)

![](images/Cloud/Aspose.Words.e650799a-1137-4e9d-91c4-04daf8c20ba7.008.png)

![](images/Cloud/Aspose.Words.e650799a-1137-4e9d-91c4-04daf8c20ba7.009.png)

![](images/Cloud/Aspose.Words.e650799a-1137-4e9d-91c4-04daf8c20ba7.010.png)

![](images/Cloud/Aspose.Words.e650799a-1137-4e9d-91c4-04daf8c20ba7.011.png)

![](images/Cloud/Aspose.Words.e650799a-1137-4e9d-91c4-04daf8c20ba7.002.png)

![](images/Cloud/Aspose.Words.e650799a-1137-4e9d-91c4-04daf8c20ba7.012.png)

![](images/Cloud/Aspose.Words.e650799a-1137-4e9d-91c4-04daf8c20ba7.013.png)



# **Cloud Service Models**
- The National Institute of Standards and Technology (NIST) define three Service Models of how cloud services can be offered:
  - IaaS Infrastructure as a Service
  - PaaS Platform as a Service
  - SaaS Software as a Service
- Large cloud server providers offer multiple models
- The three models define where the customer and provider areas of responsibility are, and at what level the customer gains access.
- The three models build on top of one another.

![](images/Cloud/Aspose.Words.e650799a-1137-4e9d-91c4-04daf8c20ba7.014.png)

![](images/Cloud/Aspose.Words.e650799a-1137-4e9d-91c4-04daf8c20ba7.009.png)

![](images/Cloud/Aspose.Words.e650799a-1137-4e9d-91c4-04daf8c20ba7.015.png)

![](images/Cloud/Aspose.Words.e650799a-1137-4e9d-91c4-04daf8c20ba7.016.png)

![](images/Cloud/Aspose.Words.e650799a-1137-4e9d-91c4-04daf8c20ba7.017.png)

#
# **Cloud Deployment Models**
- The NIST define four Cloud Deployment Models:
  - Public Cloud
  - Private Cloud
  - Community Cloud
  - Hybrid Cloud

## **Public Cloud**
‘The cloud infrastructure is provisioned for open use by the general

public. It may be owned, managed, and operated by a business, academic, or government organization, or some combination of them.

It exists on the premises of the cloud provider.’ NIST


Examples
All the Cloud Providers you know about, like:

- AWS
- Microsoft Azure
- IBM Bluemix
- Salesforce

This is by far the most common deployment model


## **Private Cloud**
- ‘The cloud infrastructure is provisioned for exclusive use by a single organization comprising multiple consumers (e.g., business units). It may be owned, managed, and operated by the organization, a third party, or some combination of them, and it may exist on or off premises.’ NIST 
- Private Cloud works the same way as Public Cloud, but the services are provided to internal business units instead of to external public enterprises.

**How is Private Cloud Different than On Prem?**

- Private Cloud fulfils the Cloud ‘Essential Characteristics’:
  - On-Demand Self-Service
  - Rapid Elasticity
  - Broad Network Access
  - Resource Pooling
  - Measured Service
- With the traditional On Premises model, a business unit orders a new server by raising a ticket with the IT department. The server is then provisioned and configured by the server, network, and storage teams as separate manual processes.
- With Private Cloud, a business unit orders a new server typically through a web portal. The server is then completely automatically provisioned without requiring manual intervention.
- The company will use automation software such as Cisco UCS Director
- DNA Center can be used as an SDN controller
- Private Cloud is most suitable for large companies where the long term ROI and efficiency gains can outweigh the initial effort and cost to set up the infrastructure and automated workflows

Private Cloud Examples

- Companies with Private Cloud don’t usually advertise the fact because it’s, well, private.
- A well known example is the US Department of Defense on Private Cloud provided by AWS. This is an example of Private Cloud owned, managed, and operated by a third party.




**Not Really ‘Private Cloud’**

- Public Cloud IaaS providers will sometimes market Dedicated Servers as Private Cloud because the underlying servers are dedicated for a particular customer
- This is not true Private Cloud however as the supporting network infrastructure is shared with other customers


## **Community Cloud**
- ‘The cloud infrastructure is provisioned for exclusive use by a specific community of consumers from organizations that have shared concerns (e.g., mission, security requirements, policy, and compliance considerations).’ NIST
- This is the least common deployment model. It is sometimes used in government environments

## **Hybrid Cloud**
- ‘The cloud infrastructure is a composition of two or more distinct cloud infrastructures (private, community, or public) that remain unique entities, but are bound together by standardized or proprietary technology that enables data and application portability (e.g., cloud bursting for load balancing between clouds).’ NIST
- Companies with limited Private Cloud infrastructure may ‘cloud burst’ into Public Cloud for additional capacity when required
- A company could also have Private Cloud at their main site and use Public Cloud for their Disaster Recovery location

# **Cloud Advantages** 
- Scalability
- Business Agility
- Cost Efficiency
- Competitive Advantage
- Productivity
- Availability and Reliability
- Cost
