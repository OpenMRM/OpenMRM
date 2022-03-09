# Source control for Open MRM
The Project plans to use a GitHub as its source code, documentation and artifact repository.

Issues and Pull Requests will be used to manage contributions as described below:

# Issues

* Issues will be used to describe and track issues from users, code contributors and others
* Issues will be triaged with labels
* Labels will help identify what the issues is so we find potential 
  /kind  
    (options: question, feature, bug)
  /area 
    (options: installation, agent, CCS, Services Protocol,) 
  /implementation 
    (options: finance, healthcare, kubeflow, etc.)

# Pull Requests

* Pull Requests (PR) will be used to describe, track, approve and merge code and documentation contributions
* PR will be triaged with labels
* Labels will help identify potential support
  /kind  
    (options: question, feature, bug)
  /area 
    (options: installation, agent, CCS, Services Protocol,) 
  /implementation 
    (options: finance, healthcare, kubeflow, etc.)

# Reviews and Commit approvals

* Pull Requests will be submitted by committers
* Pull Request will require reviews and approvals
* Reviewers will have reviewing rights based on the directory structure
* Contributors can request reviewer rights for a directory
* Approvers can approve adding contributor rights to a contributor
* Approvers will have approval rights based upon the directory structure
* Contributors can request approval rights for a directory
* Approvers can approve adding approval rights to a contributor
* Reviews will be provided by Approvers
* Reviews will provide /lgtm
* Approvers will provide /merge


# Git Repository Structure

The Git repository will need an extensible directory structure. The plan is to use the root directory for the readme and community information including the Code of Conduct, licensing, structure, process, etc. Sub modules will be used.  The structure for the submodules is TBD.  The following provides a proposal which so that the code and artifacts will be managed in sub modules.


MRM/MRM

MRM/Agent

MRM/CCS

MRM/ServicesProtocol

MRM/POC1

MRM/POC1/Readme

MRM/POC1/Agent

MRM/POC1/CCS

MRM/POC1/ServicesProtocol

MRM/POC1/GettingStarted

MRM/POC1/Releases

