.. _bigip_provision:


bigip_provision - Manage BIG-IP module provisioning
+++++++++++++++++++++++++++++++++++++++++++++++++++

.. versionadded:: 2.3


.. contents::
   :local:
   :depth: 1


Synopsis
--------

Manage BIG-IP module provisioning. This module will only provision at the standard levels of Dedicated, Nominal, and Minimum. While iControl SOAP additionally supports a Custom level, this level is not supported by this module.


Requirements (on host that executes module)
-------------------------------------------

  * f5-sdk


Options
-------

.. raw:: html

    <table border=1 cellpadding=4>
    <tr>
    <th class="head">parameter</th>
    <th class="head">required</th>
    <th class="head">default</th>
    <th class="head">choices</th>
    <th class="head">comments</th>
    </tr>
            <tr>
    <td>level<br/><div style="font-size: small;"></div></td>
    <td>no</td>
    <td>nominal</td>
        <td><ul><li>dedicated</li><li>nominal</li><li>minimum</li></ul></td>
        <td><div>Sets the provisioning level for the requested modules. Changing the level for one module may require modifying the level of another module. For example, changing one module to <code>dedicated</code> requires setting all others to <code>none</code>. Setting the level of a module to <code>none</code> means that the module is not run.</div></td></tr>
            <tr>
    <td>module<br/><div style="font-size: small;"></div></td>
    <td>yes</td>
    <td></td>
        <td><ul><li>afm</li><li>am</li><li>sam</li><li>asm</li><li>avr</li><li>fps</li><li>gtm</li><li>lc</li><li>ltm</li><li>pem</li><li>swg</li></ul></td>
        <td><div>The module to provision in BIG-IP.</div></td></tr>
            <tr>
    <td>password<br/><div style="font-size: small;"></div></td>
    <td>yes</td>
    <td></td>
        <td><ul></ul></td>
        <td><div>The password for the user account used to connect to the BIG-IP.</div></td></tr>
            <tr>
    <td>server<br/><div style="font-size: small;"></div></td>
    <td>yes</td>
    <td></td>
        <td><ul></ul></td>
        <td><div>The BIG-IP host.</div></td></tr>
            <tr>
    <td>server_port<br/><div style="font-size: small;"> (added in 2.2)</div></td>
    <td>no</td>
    <td>443</td>
        <td><ul></ul></td>
        <td><div>The BIG-IP server port.</div></td></tr>
            <tr>
    <td>state<br/><div style="font-size: small;"></div></td>
    <td>no</td>
    <td>present</td>
        <td><ul><li>present</li><li>absent</li></ul></td>
        <td><div>The state of the provisioned module on the system. When <code>present</code>, guarantees that the specified module is provisioned at the requested level provided that there are sufficient resources on the device (such as physical RAM) to support the provisioned module. When <code>absent</code>, unprovisions the module.</div></td></tr>
            <tr>
    <td>user<br/><div style="font-size: small;"></div></td>
    <td>yes</td>
    <td></td>
        <td><ul></ul></td>
        <td><div>The username to connect to the BIG-IP with. This user must have administrative privileges on the device.</div></td></tr>
            <tr>
    <td>validate_certs<br/><div style="font-size: small;"> (added in 2.0)</div></td>
    <td>no</td>
    <td>True</td>
        <td><ul><li>True</li><li>False</li></ul></td>
        <td><div>If <code>no</code>, SSL certificates will not be validated. This should only be used on personally controlled sites using self-signed certificates.</div></td></tr>
        </table>
    </br>



Examples
--------

 ::

    - name: Provision PEM at "nominal" level
      bigip_provision:
          server: "lb.mydomain.com"
          module: "pem"
          level: "nominal"
          password: "secret"
          user: "admin"
          validate_certs: "no"
      delegate_to: localhost
    
    - name: Provision a dedicated SWG. This will unprovision every other module
      bigip_provision:
          server: "lb.mydomain.com"
          module: "swg"
          password: "secret"
          level: "dedicated"
          user: "admin"
          validate_certs: "no"
      delegate_to: localhost


Notes
-----

.. note:: Requires the f5-sdk Python package on the host. This is as easy as pip install f5-sdk.


    
This is an Extras Module
------------------------

For more information on what this means please read :doc:`modules_extra`

    
For help in developing on modules, should you be so inclined, please read :doc:`community`, :doc:`developing_test_pr` and :doc:`developing_modules`.

