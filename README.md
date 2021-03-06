Mesos Cookbook
==============
Insalls and configure Mesos(<http://mesos.apache.org/>) master and slave.

Platform
------------
only support `ubuntu`

Cookbooks
----
### mesos::default(mesos::build_from_source)
install mesos(download zip from github, configure, make, make install).

### mesos::master
configure master and cluster deployment configuration files.

* `node[:mesos][:prefix]/var/mesos/deploy/masters`
* `node[:mesos][:prefix]/var/mesos/deploy/slaves`
* `node[:mesos][:prefix]/var/mesos/deploy/mesos-deploy-env.sh`
* `node[:mesos][:prefix]/var/mesos/deploy/mesos-master-env.sh`

### mesos::slave
configure slave configuration files.

* `node[:mesos][:prefix]/var/mesos/deploy/mesos-slave-env.sh`

Usage
----
please see [everpeace/vagrant-mesos](https://github.com/everpeace/vagrant-mesos).

Attributes
----------
#### mesos::default(mesos::build_from_source)
<table>
  <tr>
    <th>Key</th>
    <th>Type</th>
    <th>Description</th>
    <th>Default</th>
  </tr>
  <tr>
    <td><tt>[:mesos][:version]</tt></td>
    <td>String</td>
    <td>Version(branch or tag name at http://github.com/apache/mesos).</td>
    <td><tt>master</tt></td>
  </tr>
  <tr>
  <td><tt>[:mesos][:prefix]</tt></td>
  <td>String</td>
  <td>Prefix value to be passed to configure script</td>
  <td><tt>/usr/local</tt></td>
  </tr>
  <tr>
  <td><tt>[:mesos][:home]</tt></td>
  <td>String</td>
  <td>Directory which mesos sources are extracted to(<tt>node[:mesos][:home]/mesos</tt>).</td>
  <td><tt>/opt</tt></td>
  </tr>
  <tr>
    <td><tt>[:mesos][:build][:skip_test]</tt></td>
    <td>Boolean</td>
    <td>Flag whether test will be performed.</td>
    <td><tt>true</tt></td>
  </tr>
</table>
### mesos::master
<table>
  <tr>
    <th>Key</th>
    <th>Type</th>
    <th>Description</th>
    <th>Default</th>
  </tr>
  <tr>
    <td><tt>[:mesos][:prefix]</tt></td>
    <td>String</td>
    <td>Prefix value to be passed to configure script</td>
    <td><tt>/usr/local</tt></td>
  </tr>
  <tr>
    <td><tt>[:mesos][:ssh_opt]</tt></td>
    <td>String</td>
    <td>ssh options to be used in mesos-[start|stop]-cluster</td>
    <td><tt>-o StrictHostKeyChecking=no <br/> -o ConnectTimeout=2</tt></td>
  </tr>
  <tr>
    <td><tt>[:mesos][:deploy_with_sudo]</tt></td>
    <td>String</td>
    <td>Flag whether sudo will be used in mesos-[start|stop]-cluster</td>
    <td><tt>1</tt></td>
  </tr>
  <tr>
    <td><tt>[:mesos][:cluster_name]</tt></td>
    <td>String</td>
    <td>Human readable name for the cluster, displayed at webui</td>
    <td><tt>MyCluster</tt></td>
  </tr>
  <tr>
    <td><tt>[:mesos][:master][:zk]</tt></td>
    <td>String</td>
    <td>ZooKeeper URL (used for leader election amongst masters)</td>
    <td>(optional)</td>
  </tr>
  <tr>
    <td><tt>[:mesos][:mater_ips]</tt></td>
    <td>Array of String</td>
    <td>IP list of masters used in mesos-[start|stop]-cluster</td>
    <td>[ ]</td>
  </tr>
  <tr>
    <td><tt>[:mesos][:slave_ips]</tt></td>
    <td>Array of String</td>
    <td>IP list of slaves used in mesos-[start|stop]-cluster</td>
    <td>[ ]</td>
  </tr>
  <tr>
    <td><tt>[:mesos][:master][:ip]</tt></td>
    <td>String</td>
    <td>IP address to listen on</td>
    <td></td>
  </tr>
  <tr>
    <td><tt>[:mesos][:master][:log_dir]</tt></td>
    <td>String</td>
    <td>Location to put log files.</td>
    <td><tt>/var/log/mesos</tt></td>
  </tr>
</table>

### mesos::slave
<table>
  <tr>
    <th>Key</th>
    <th>Type</th>
    <th>Description</th>
    <th>Default</th>
  </tr>
  <tr>
    <td><tt>[:mesos][:prefix]</tt></td>
    <td>String</td>
    <td>Prefix value to be passed to configure script</td>
    <td><tt>/usr/local</tt></td>
  </tr>
  <tr>
    <td><tt>[:mesos][:slave][:master_url]</tt></td>
    <td>String</td>
    <td>[REQUIRED] mesos master url.This should be ip:port for non-ZooKeeper based masters, otherwise a zk:// </td>
    <td></td>
  </tr>
  <tr>
    <td><tt>[:mesos][:slave][:ip]</tt></td>
    <td>String</td>
    <td>IP address to listen on</td>
    <td></td>
  </tr>
  <tr>
    <td><tt>[:mesos][:slave][:log_dir]</tt></td>
    <td>String</td>
    <td>Location to put log files.</td>
    <td><tt>/var/log/mesos</tt></td>
  </tr>
  <tr>
    <td><tt>[:mesos][:slave][:work_dir]</tt></td>
    <td>String</td>
    <td>Where to place framework work directories.</td>
    <td><tt>/var/run/mesos</tt></td>
  </tr>
  <tr>
    <td><tt>[:mesos][:slave][:isolation]</tt></td>
    <td>String</td>
    <td>Isolation mechanism, may be one of: process, cgroups</td>
    <td><tt>cgroups</tt></td>
  </tr>
</table>


Contributing
------------

1. Fork the repository on Github
2. Create a named feature branch (like `add_component_x`)
3. Write you change
4. Write tests for your change (if applicable)
5. Run the tests, ensuring they all pass
6. Submit a Pull Request using Github

License and Authors
-------------------
* Author:: Shingo Omura everpeace@gmail.com

Copyright:: 2009-2013 Shingo Omura, All rights reserved.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
