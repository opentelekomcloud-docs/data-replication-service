:original_name: drs_08_0088.html

.. _drs_08_0088:

Creating a Custom Policy
========================

Custom policies can be created to supplement the system-defined policies of DRS.

You can create custom policies in either of the following ways:

-  Visual editor: Select cloud services, actions, resources, and request conditions. This does not require knowledge of policy syntax.
-  JSON: Create a policy in JSON format or edit the JSON strings of an existing policy.

For details about how to create a custom policy, see Identity and Access Management User Guide. The following describes examples of common DRS custom policies.

Example Custom Policies
-----------------------

-  Example 1: Allowing users to create DRS instances

   .. code-block:: text

      {
          "Version": "1.1",
          "Statement": [{
                      "Action": ["drs:migrationJob:create"],
              "Effect": "Allow"
          }]
      }

-  Example 2: Denying DRS instance deletion

   A policy with only "Deny" permissions must be used in conjunction with other policies to take effect. If the permissions assigned to a user contain both "Allow" and "Deny", the "Deny" permissions take precedence over the "Allow" permissions.

   The following method can be used if you need to assign permissions of the **DRS FullAccess** policy to a user but you want to prevent the user from deleting DRS instances. Create a custom policy for denying DRS instance deletion, and attach both policies to the group to which the user belongs. Then, the user can perform all operations on DRS instances except deleting DRS instances. The following is an example of a deny policy:

   .. code-block:: text

      {
          "Version": "1.1",
          "Statement": [{
              "Action": ["drs:migrationJob:delete"],
              "Effect": "Deny"
          }]
      }
