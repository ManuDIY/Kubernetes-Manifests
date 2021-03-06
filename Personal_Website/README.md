## Personal Website

<p align="center">
  <img src="https://raw.githubusercontent.com/zimmertr/Kubernetes-Manifests/master/Personal_Website/screenshot.png" width="800">
</p>

**Summary:**

These manifests are used to deploy an instance of my *Personal Website*. 

Approximate Deployment Time: 1-5 minutes

**Requirements:**  

1. Load Balancer integration so that the Service can expose the pods.
2. NFS Server to which Kubernetes can bind Persistent Volumes.
3. Directory structsure created on the NFS Endpoint you specify in `vars.yml`.
4. Python modules required to use the k8s [Ansible module](https://docs.ansible.com/ansible/latest/modules/k8s_module.html).    
    * pip install openshift kubernetes pyyaml 
    * If you're on MacOS, you might have to do [this](https://github.com/ansible/ansible/issues/43637#issuecomment-443495763) instead.

**Instructions:**  

1. Modify `vars.yml` with parameters according to your environment.
2. Create the necessary directories defined in `vars.yml` on your NFS server.
    * If you use enable Google Analytics tracking and/or Weather information in the terminal, fill in the related parameters in `vars.yml`. If you do not, these features will not be available. 
3. Execute the playbook: `ansible-playbook provision.yml`.  
4. Navigate to http://host.name:80/ to access the software. 

**TODO:**

1. Fix the `weatherbot` container to have an API-like relationship with the `website` container instead of sharing information via a text file.

**Deletion:**  

1. You can roll back this deployment with the `delete.yml` playbook: `ansible-playbook delete.yml`.
    * Please note, this will not remove the deployed namespace because I could not be sure you didn't specify an existing namespace. I would hate to delete your `default` for example. So you must manually clean that up. `kubectl delete ns >namespace name<`
   
