# Open MRM Project
Open Source Model Risk Management Project (Open MRM Project)

# TL;DR
This Request for Comment [(RFC)](https://docs.google.com/document/d/1qNS2VG70v4uoS5_8MU66aVGIKcKOB_TzMfATULm9QD0/edit#) defines an open source software project for a composable Model Risk Management (MRM) services architecture with the explicit purpose of sharing MRM best practices for managing Machine Learning (ML) models.  The RFC defines a Proof of Concept (POC) that includes a unique identity token and a Smart Agent, which will be embedded within each model, and a Server that will manage model usage and collect usage data that is transmitted by the Smart Agent into a central repository. The POC will provide hands-on feedback of the RFC’s record schemas, libraries and application level APIs.

# The Problem
As Machine Learning model adoption expands, so does the associated model risk, and organizations are struggling to track, control and understand their ML model usage.   Most leading organizations have developed formal governance policies for their ML model use, and these policies are implemented and audited by three lines of (internal) defense (LOD): model owners (developers, users, model supervisors), model risk management (validators) and internal audit (IA).  In addition, governing bodies, i.e. the U.S. Federal Reserve and the Office of the Comptroller of the Currency, have produced guidelines, i.e. [SR11-7/OCC2011-12](https://www.federalreserve.gov/supervisionreg/srletters/sr1107a1.pdf) and the Comptroller’s Handbook for MRM, for implementing an effective and rigorous model risk management framework.  

Per SR 11-7, the implementation of MRM frameworks is part of the overall responsibilities of any bank’s board and senior management, and should fit within the broader risk management of the organization. As these guidelines are broadly stated and not prescriptive, organizations must coordinate their internal groups to interpret the guidelines and then implement them through governance protocols and procedures. While there is flexibility in the choice of protocols and procedures across institutions, there is an expectation of a uniformity of application of these protocols and procedures within any given organization. The large variation in applications and underlying tooling across AI/ML models presents significant barriers to automated extraction and use of the information necessary to prove compliance with these protocols and procedures; this poses challenges to the standardization of risk reporting, inventory management, and risk mitigation strategies. This information is required for both internal and external MRM reviews.  

As the examples below demonstrate, the number and types of AI/ML platforms, languages, algorithms, and development environments that will benefit from a model usage taxonomy continue to expand:

* Frameworks: 
  * Tensorflow, Keras, PyTorch, XGBoost, Catboost, MxNet, Logistic Regression, Support Vector Machine, Sklearn 
* Activation functions: 
  * Binary Step Function, Linear Function, Sigmoid, Tanh, ReLU, Leaky ReLU, Parameterised ReLU, Exponential Linear Unit  
* Notebooks and Integrated Development Environments (IDEs): 
  * JupyterLab, R-Studio. VSCode, NetBeans, Eclipse, Pycharm, RStudio 
* ML Platforms & managed services: 
  * Sagemaker, Databricks, AzureML, Vertex, Kubeflow, MLFlow, H2O, Seldon, KServe 

Unfortunately, many organizations are challenged to understand how the guidelines should be applied to their specific infrastructures, and to apply industry best practices to implement efficient systems and processes in this rapidly changing environment.  In addition, the requirements for a rigorous model risk management platform can vary depending on the organization, especially as fully SR 11-7 compliant MRM implementations can include a number of services such as model inventory, dashboards, reporting, approval tracking, access control, data management, bias detection and risk protection.  

For many organizations, the resource requirements needed to adequately address the risks associated with the current state of affairs are beyond their means;  this RFC proposes the creation of an open source community project to deliver on these critical future state goals in a significantly more cost-effective manner:

# Why invest in an MRM open source community project

#### Builds Community consensus on best practices, architectures, and requirements
   * Organizations need guidance on the type and quantity of the most important usage data fields to be collected from a model by a Smart Agent.  They also need guidance on what features are required in an MRM services architecture.

#### Reduces liability of independent system development.
   * Industry review and comments enable more analysis of requirements and liabilities.  This process will not provide legal protections, but the process of peer review does help in sharing industry-wide best practices in an appropriate manner.

#### Increases industry penetration of automation for governance. 
   * Although many may agree that increased MRM adoption is in the public good, and will also benefit institutions and regulators, the technical and procedural requirements to build a functional MRM implementation are complex, costly and specific to each organization. 

#### Standard interface enables interoperability and composibility. 
   * Depending on timing, budgets and resources, a large organization may need interoperability between open source, homegrown and proprietary MRM systems.  

#### Flexibility to build or buy the MRM services.
   * Organizations have unique requirements and will benefit from  options to either buy or build MRM services such as model inventory, dashboard configuration, report generation, approval tracking, access control, data management, bais detection and risk protection.   

An open source MRM architecture can support popular ML frameworks, activation functions, model serving runtimes and disparate ML platforms, all of which will help organizations avoid lock-in.  

## Step 1 - Define open source schemas, libraries and APIs
This RFC recognizes that building an entire MRM system is a comprehensive and costly commitment, especially as a variety of MRM services will need access to reliable, accurate and complete data on model usage.  Therefore this paper proposes starting with the instrumentation and control of model usage via a Smart Agent, as this is a critical function that is not defined in open source today.   A high level functional overview of this architecture is proposed as follows: 

<img width="631" alt="Screen Shot 2022-02-27 at 6 23 45 PM" src="https://user-images.githubusercontent.com/10553232/155906682-758196d0-e695-4826-9891-589e53068afc.png">

In the RFC’s agent/server architecture, an active Smart Agent will reside within each model.  The Smart Agent will support two main functions: 

1) producing a record for each model execution event  (Smart Agent record) 
2) enabling remote control of the model (i.e. start, hard stop, graceful stop, testing, reporting, logging).  

The Collection and Control Server (CCS) will have several functions:

1) The CCS receives and stores the Smart Agent record.  
2) The CCS appends and modifies additional information to create a CCS record.   
3) The CCS issues control messages to the model. 
4) The CCS provides the data from the CCS records to other MRM services.  

The Agent and the CCS are defined by record schemas, libraries and application level APIs.   The Enterprise Management Server is an optional component which potentially functions as a proxy from the CCS to the MRM Services and enables advanced enterprise features.  The MRM Services can leverage an open protocol to interface with the Enterprise Management Server, or directly with the CCS (not shown).   The MRM Services provide MRM functions i.e. inventory, dashboards, report generation, bias or risk monitoring, and are designed to be interoperable software services that can be added as needed.   The MRM Services could be built or purchased depending on the user’s requirements and timeline.

## Step 2 - Gathering feedback from the POC
This community project is designed to support open source development and discussion balanced with input from hands-on experimentation(s) from different organizations.  Beyond implementing the proposed Smart Agent/CCS functionality, the POC(s) can include an integration with an MRM Inventory Service component as a demonstration of the broader MRM services architecture.   

Although the long-term goal is to support interchangeable pluggable MRM components and leverage dependencies with a high degree of extensibility, there is a recognition that a short term hands-on POC will require some critical early decisions.  As an initial step, this paper proposes building the Smart Agent and integrating it with a Collection and Control Server (CCS) that will also serve as a central repository for model usage data.  The CCS will also support the integration with client’s or vendor’s preferred MRM Inventory services.  As a reference point, Figure 2 provides a high-level architecture diagram of the POC and the details of this implementation are expected to be defined in a follow-on document.

<img width="680" alt="Screen Shot 2022-03-05 at 10 18 33 AM" src="https://user-images.githubusercontent.com/10553232/156893373-5bb4fc52-c20b-46af-afbb-e5e0df5d667f.png">

### Next Steps 
Realizing a rigorous, SR 11-7 compliant MRM implementation is a complex and extensive undertaking, and many organizations will have different requirements (and opinions).  It is not expected that a single open source implementation can fully satisfy all requirements. This project is designed to provide a starting place for discussion and experimentation, and promote iteration for an open source MRM services architecture. 

### Request for Comments

The Open MRM RFC and its appendix provide a structure and details on the Open MRM architecture.   If you would like to review and potentially comment on the Open MRM RFC and appendix, please sign-up
 [here](https://forms.gle/Du2r2jgeVbqbEncY8).   You will promptly receive access to the document and commenting process, which will be open for the next 90 days.   

Additionally we invite you to get involved in the Open MRM Community by:

* Joining the Slack channel: OpenMRM.slack.com
* Joining the GitHub project: [contributor details](https://github.com/OpenMRM/OpenMRM/blob/main/structure.md)	
* Joining a Community meeting: Initial meeting Friday, March 25 at 10am CST

