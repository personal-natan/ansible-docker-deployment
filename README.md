WORKING WITH THIS AUTOMATION SCRIPT

1. setup your configuration in ansible.cfg
   ```
   inventory = inventory

   host_key_checking = False

   deprecation_warnings = False

   remote_user = $user
   private_key_file = ~/.ssh/id_rsa #(your private key path)
   ```
2. set up inventory file, your destination server. Put the IP there.

3. Now set up your global variables in group_vars/all.yml
   ```
   services:
   - { 
        name_service: $servicename,  
        image: $imagetag,
        port: $app_port,
        publish_port: $publish_port,
        net_mode: $network_mode,
        mount_dst: $mount_destination,
        mount_src: $mount_source,
        mount_type: $mount_type,
        replica: $replica
     }

   - { 
        name_service: $servicename,   
        image: $imagetag,
        port: $app_port,
        publish_port: $publish_port,
        net_mode: $network_mode,
        mount_dst: $mount_destination,
        mount_src: $mount_source,
        mount_type: $mount_type,
        replica: $replica
     }

   volumes:
   - {
       name: $volume_name,
       backup: {
         # turn True when you need to backup the volume in case there is migration
         create_backup: $bool,
         # where you'd like to store the backup file
         dest: $path_destination 
       }
     }

   delete_services: 
     - $servicename

   delete_volumes: 
     - $volume_name 
   ```
4. Run manually the workflow base on this order
   - docker-prep.yml ( this step for installing all dependencies related to docker )
   - docker-deploy-svc.yml ( deploy the service )
   - docker-log.yml ( optional, to check description of the container )
