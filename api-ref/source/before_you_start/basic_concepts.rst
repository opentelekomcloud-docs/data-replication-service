:original_name: drs_api_0113.html

.. _drs_api_0113:

Basic Concepts
==============

Domain
------

A domain is created after your registration. The domain has full access permissions for all of its cloud services and resources. It can be used to reset user passwords and grant user permissions. The domain is a payment entity and should not be used directly to perform routine management. For security purposes, create users and grant them permissions for routine management.

IAM User
--------

An IAM user is created using a domain to use cloud services. Each IAM user has its own identity credentials (password and access keys).

The domain name, username, and password will be required for API authentication.

Region
------

A region is a geographic area in which cloud resources are deployed. Availability zones (AZs) in the same region can communicate with each other over an intranet, while AZs in different regions are isolated from each other. Deploying cloud resources in different regions can better suit certain user requirements or comply with local laws or regulations.

AZ
--

An AZ comprises one or multiple physical data centers equipped with independent ventilation, fire, water, and electricity facilities. Computing, network, storage, and other resources in an AZ are logically divided into multiple clusters. AZs within a region are interconnected using high-speed optical fibers to allow users to build cross-AZ high-availability systems.

Project
-------

A project corresponds to a region. Default projects are defined to group and physically isolate resources (including computing, storage, and network resources) across regions. You can grant users permissions in a default project to access all resources in the region associated with the project. If you need more refined access control, create subprojects under a default project and purchase resources in subprojects. Then you can assign users the permissions required to access only the resources in the specific subprojects.


.. figure:: /_static/images/en-us_image_0000001782191918.png
   :alt: **Figure 1** Project isolating model

   **Figure 1** Project isolating model
