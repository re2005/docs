# BitDust Change Log



2018-11-10 Veselin Penev [penev.veselin@gmail.com](mailto:penev.veselin@gmail.com)

* ported to Python3.6 finally (Python2.7 also supported) !!!
* speed up raid workers (Stanislav Evseev)
* switched from parallelp to the built-in multiprocessing (Stanislav Evseev)
* turn on proxy server by default for all nodes, updated seed nodes
* built more unit tests
* "make test" command will also execute "python bitdust.py install" first
* use global python to run unit tests
* run unit tests on travis
* transition from pickle to json
* new regression tests based on docker containers (Stanislav Evseev)
* CI/CD integration with travis
* detect current python version in deploy script and use it
* added system.deploy module to isolate everythng related to "python bitdust.py install" command
* Add chat-history endpoint (Anton Grishun)
* slow down DHT traffic
* added space_donated(), space_consumed() and space_local() methods to REST HTTP API
* added api method identity_backup(), tested recover identity
* bug fix : correctly load/save list of my suppliers
* randomize tcp, udp, http, dht and blockchain port numbers during startup
* Added environment variable to access to internal api interface
* added bitrex.ai to dht seed nodes (by Renato Cardoso)
* added CodernityDB3 fork to code base



2018-07-28 Veselin Penev [penev.veselin@gmail.com](mailto:penev.veselin@gmail.com)

* added more known id servers
* added smoketestdht in Makefile
* added event "shared-list-files-received"
* added events "share-connected", "share-disconnected"
* added events "private-key-shared" and "private-key-share-failed"
* add simple health-check method
* isolated SSL dependecies in old/unused methods in lib.net_misc
* make possible to register new identity on local ID server
* store public keys in OpenSSH format and private keys in PEM
* use pickle instead of base64 to serialize encrypted data
* backward incompatible !!!!!!!!!!!!!!!! : reimplement encryption, use pycryptodomex instead of pycrypto, bump twisted version in requirements
* clean up, removed old "UI experiments" based on Django framework
* installing virtualenv isolated
* updated blockchain/trinity/deploy_linux.sh
* pyethapp is dead, testing trinity which is python3.6
* experiments with pyethapp blockchain tool
* added file/download/v1 api method
* encoding fix: always set UTF8 as default locale
* executable file name fix in few places to make windows electron platform working
* added api.shell() method to be able to debug in real time
* added task for tracking network statuses and reconnect network service
* updated list of seed nodes
* wraping stored data with extra layer when supplier returning back saved files in order to route it correctly
* sending pub keys to suppliers when required
* loading suppliers of other known customers at start up
* added callback_id in the automat class
* temporary disabled "CRITICALLY_OFFLINE" supplier dismiss fearure
* added `all_customers` parameter to api.file_list() API
* limit twisted<18 in requirements.txt
* added timer fallback in network_connector()
* added method API method network/details
* added api method user_status_check()
* added api.identity_list() method
* rebuilt dht service and added key-value expiration flow
* added cancel() method to service_supplier_relations() to be able to clean up junk dht records
* updated file_upload/file_download API methods so they will be able to open share before start
* improving files synchronization logic
* disabled services/udp-transport by default, services/proxy-transport should be used now by default
* stop publishing "supplier-file-modified" event, more smart fire_hire()
* added share_list() and share_create() api mothods, adjusted key_id format validation
* added id server bitrex.ai:8084
* shared file download is working !!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
* fixed api.message_send(), packet_in.process() to be able to cache input packet creator identity
* in service_supplier() external customer must be able to request Data()
* service_supplier() able to send shared data to external customer
* bump dht protocol version to 5
* publishing my active eccmap in dht relations
* added DetectSupplierPosition() to be able to connect to external suppliers
* bump dht protocol version to 4
* modified stun client code to use randomized udp and dht port numbers
* added lg.args() method, testing DHT methods
* added DHT methods to work with validated json data
* added clean up in dht_relations()
* refactored Files() command - must be encrypted now
* must be able to request 0 bytes from supplier
* working with file sharing



2018-04-16 Veselin Penev [penev.veselin@gmail.com](mailto:penev.veselin@gmail.com)

* refactoring/improvements/new api methods, building file share methods, supporting new UI based on electron framework
* switched from restore() to restore_worker()
* added data_receiver() machine
* updated packet_out() : use cached copy of the remote identity only if it is fresh - if older than 60 sec then cache again
* randomized backups fs id
* added api methods to exchange json messages
* added api methods to get/set my nickname
* improved performance of api.user_search()
* added rest method for adding/removing users from list of contacts
* save backup index in service_customer()
* also storing locally a list files from other customers
* processing ListFiles() command also in service_customer()
* added service_shared_data(), testing shared_access_donor() machine
* added api.share_open() and api.share_history() interfaces
* added Packets field to signed.Packet to store outgoing transfers
* building shared_access_coordinator()
* added response timeout callback methods to packet_out and catching that in key_audit() now
* able to audit master key as well
* added api.transfers_list() to be able to test/debug file uploads/downloads process
* destination_folder is not a mandatory in api.file_download_start()
* added api.key_audit() method
* added AuditKey() command, working with key_ring, added method to test validate keys on remote machines
* added access/shared_access_coordinator.py
* rework event id format in the p2p queue, publish events from the blockchain
* working with blockchain, registering own identity in the blockchain if possible (mine a block if not enough coins)
* miners should only generate blocks if some transactions are pending
* Added service_blockchain() based on PyBC open source project - basic implementation of blockchain technology
* added file_download_start() and file_download_stop()  to REST HTTP API
* set normalize_key_alias=True everywhere : force to send key_alias in packetID
* updated ListFiles()/Files() commands so that they also processing key_alias parameter
* change storage location for customer's file : also depend on key_alias
* handling of Event() packets in service_p2p_notifications() only
* add logging in automat.startTimers()
* Big change! refactor p2p services requests : use generic json structures instead of plain strings
* added methods to connect producer with given queue
* added api.queue_list()
* added global_id.ParseGlobalQueueID(queue_id) method, fix in my_keys
* make api.network_connected() workin properly and return valid status based on p2p_connector().state
* improved api.service_restart() method, added wait_timeout parameter with default value 10 seconds
* generate events when your contacts got changed
* added flexibility to crypt.signed.Packet : you can use specific key to sign your data now, not only your master key
* finilized design of the queue_id: {queue_alias}&{owner_id}&{supplier_id}
* set service_p2p_notifications enabled by default
* change dependecy for service_supplier - it must depend on service_p2p_notifications also
* add CORS to REST HTTP API, work with p2p_queue, fixes
* added /event/send/<event_id>/v1 API HTTP method
* added response_timeout argument to packet_out()
* added Event() to p2p.commands
* skip command handling in p2p_service, logic distributed to the services
* added p2p_queue.py, refactoring
* publish events from id_restorer() and id_registrator()
* added api.event_listen(), possible to publish event when state machine change state, work on api.service_restart()
* modified initializer() machine logic: start bitdust process even if local identity is not exist, added API methods to create/recover identity
* disabled Django WEB UI interface, we are building new UI based on Electron
* added service_p2p_notifications()



2018-01-14 Veselin Penev [penev.veselin@gmail.com](mailto:penev.veselin@gmail.com)

* added id server blog.bitdust.io, removed id server whmcs.whois.ai
* fixed DHT init/connect scripts, 
* limit twisted and django versions in requirements, set --index-url=https://pypi.python.org/simple/ in deployment script
* proper handling customer location of ".bitdust" folder



2017-11-27 Veselin Penev [penev.veselin@gmail.com](mailto:penev.veselin@gmail.com)

* added few options in services/identity-propagate/ branch
* updated id_registrator() to be able to contol your identity sources via settings
* now identitycache will erase all local files on startup
* added "identity server" in command line interface to run id server locally
* added "identity backup" in command line interface
* added setup.py
* added git mirror on: dev.bitdust.io/code/devel (dev)
* added git mirror on: bitbucket.org/bitdust_io/devel (bitbucket)
* added git mirror on: gitlab.com/bitdust/devel (gitlab)
* added api /key/*/v1 REST methods, tested again key_ring sharing
* added api /config/*/v1 REST methods
* added txrestapi, added REST HTTP server for serving api.* methods in interface/rest_http_server.py, updated settings
* get rid of stun_client_RFC3489 dependency! only STUN from BitDust nodes now
* removed shtoom and stun_rfc_3489 files from repo
* added list of known id servers in idserver WEB front-end
* added api.network_stun() method to detect and report your current external IP
* added new api.message_*() methods for further development of the GUI
* added chat/message_keeper.py to store message history
* fixes in service_identity_server()
* fixes/imporvements in identitycache.py
* fixes/improvements related to global id
* fixes in lookup.py
* fixes in api.file_create()
* fixes in cmd_deploy()
* fixes in backup_fs.py
* fixes in transport/proxy/
* fixes in transport/tcp/
* updated help.py



2017-10-31 Veselin Penev [penev.veselin@gmail.com](mailto:penev.veselin@gmail.com)

* added known id server at veselin-p2p.ru
* changes in bppipe.py : store files and folders in tar archive with modified names
* error fallback flow added in restore() automat
* MAJOR CHANGE !!! ALL Enrypted customers data stored on suppliers is PUBLICLY SHARED now!
* added feature : encrypt private message with recipient master key or another known key
* bug fix in id_registrator()
* fixes in chat, more transport logs
* removed id serverd on bitdust.io:8084
* adjusted default settings : run proxy transport by default
* fixes in service_nodes_lookup(), service_proxy_transport()
% jqchat and UI fixes
* updated interface.ftp_server according to new api interface methods
* added api.file_*() commands
* removed api.backup_*() commands
* removed api.restore_*() commands
* added userid/global_id.py
* BOOM! backupID/pathID format change: 0/0/1/0/F20131120053803PM -> alice@idhost.org:0/0/1/0/F20131120053803PM
* added service_supplier_relations()
* cmd line fixes for "files" command



2017-08-23 Veselin Penev [penev.veselin@gmail.com](mailto:penev.veselin@gmail.com)

* added colors to terminal logs
* added "service_keys_registry" request in the API key_share() method flow
* added private keys managment commands to API methods
* storing catalog index in json format now
* store key_id in the catalog
* implemented multiple encryption/decryption keys in backup index
* added access/key_ring.py
* added service_keys_registry()
* added local FTP server and FTP interface bridge to access distributed data via FTP client
* added Query class to contract_chain_node
* software should be autmatically restarted after receiving an update
* added logging to git_proc, git_proc will start in 30 sec after startup
* changed "git reset --hard" to "git rebase origin/master" in git_proc.py
* added coins_index.py, working on coins storage, codernity db indexes now are located in the source code
* added added contract_chain_node.py
* fix in accountant_node() to prevent infinite loop
* added contract_chain_consumer() automat
* added service_contract_chain()
* added service_customer_contracts()
* added service_supplier_contracts()
* added state machine p2p_service_seeker()
* added simple global events system with listeners
* added Coin() and RetreiveCoin() commands
* change in broadcaster_node() automat, improved lookup and dht code, default N of broadcasters set to 3
* fix in storage/backup_matrix.py
* update help/usage, added "install" command to cmd_line interface
* setup a virtual environment folder in ~/.bitdust/venv/ to isolate BitDust software from system Python
* added one seed node
* started playing with Ethereum, continue working on contracts chains


2017-03-04 Veselin Penev [penev.veselin@gmail.com](mailto:penev.veselin@gmail.com)

* migration of genezis nodes to another vps machines
* added new configs under api/json-rpc-server/
* bug fix in restore backup flow
* removed unused id server conf scripts/docs, a new doc page added instead
* hot fix in logging
* added customer_assistant() automat to service_customer_support()


2016-12-14 Veselin Penev [penev.veselin@gmail.com](mailto:penev.veselin@gmail.com)

* improve gui, added progress bars for in/out streams
* huge changes in UPD streaming: improve performance, stability - it is working now actualy!
* bug fixes in TCP transport as well
* pep8 auto fixes for all .py files
* added index_synchronizer() machine to replace backup_db_keeper()
* remove old unused options from settings
* adjust packet_out automat
* adjust events in contact_status automat
* added another packet type (Command) for proxy transport : Relay()
* keep working on proxy transport


2016-10-23 Veselin Penev [penev.veselin@gmail.com](mailto:penev.veselin@gmail.com)

* bug fixes in settings and fire_hire machine
* updated README
* start working on crypto coins


2016-09-18 Veselin Penev [penev.veselin@gmail.com](mailto:penev.veselin@gmail.com)

* publish Python sources under GNU AGPL v3!


2016-09-04 Veselin Penev [penev.veselin@gmail.com](mailto:penev.veselin@gmail.com)

* added nodes_lookup() service
* added broadcasting() service
* added broadcast_listener() state machine
* added broadcaster_node() automat
* added broadcasters_finder() state machine
* fixes in git update procedures
* updated employer() service dependencies
* slow down bptester process a little bit
* more clean shutdown of all state machines
* `bitdust api` will print all api methods in cmd line
* fix loging in network_connector()
* fix service_udp_transport() - now it should finish stun process firstly and then go further
* modified "integrate" command, it should not create a file but print to stdout


2016-07-16 Veselin Penev [penev.veselin@gmail.com](mailto:penev.veselin@gmail.com)

* added text chat via command line
* bug fix in UDP transport
* added scripts to build commits history
* lots new API methods
* made port to Mac OS
* updates in ubuntu package


2016-05-04 Veselin Penev [penev.veselin@gmail.com](mailto:penev.veselin@gmail.com)

* built a new Web Site for BitDust project: https://bitdust.io
* new project Logo!
* lots methods added to API
* updated/improved command line interface
* made a stable port for MacOS
* fixed several major bugs in p2p networking code
* switched software updating to use "git" - distribute Python sources to end-users
* created a new Windows installer archive
* continue working on new GUI based on Django


2015-07-05 Veselin Penev [penev.veselin@gmail.com](mailto:penev.veselin@gmail.com)

* a lot of changes in the code, many things were turned off temporary
* switched API to JSON interface finally at interface/jsonrpc_server.py
* interface/cmd_line_json.py now uses lib.jsontemplate module to render content
* added Django to the project - now GUI interface is using WEB Browser (I was thinking about that stuff in 2010!)
* added Bootstrap to make a simple and nice looking design
* created jqchat and several other Django apps in the bitdust/web/ folder
* created a new deployment script : bitdust/deploy/windows_devel
* created a new binary installer : bitdust/deploy/windows_innosetup
* oh! by the way! The project was renamed from BitPie.NET to BitDust!


2014-11-23 Veselin Penev [penev.veselin@gmail.com](mailto:penev.veselin@gmail.com)

* KEY FEATURE: software core is transformed into a system of interrelated services
* made upgrade on stun client - multiple stun requests at same time to increase performance
* changed user settings engine, now it is splited on single files in sub folder: .bitdust/config/
* many fixes in GUI and command line interface
* hash method was changed from MD5 to SHA1 
* added a small feature - can request a single random packet for given backup from GUI


2014-10-21 Veselin Penev [penev.veselin@gmail.com](mailto:penev.veselin@gmail.com)

* fixed messages - p2p chat is working now! 
* did small fixes in: GUI, DHT code, API
* changed UDP PING timeout again, from 1 minute to 30 seconds


2014-10-17 Veselin Penev [penev.veselin@gmail.com](mailto:penev.veselin@gmail.com)

* a bug fix in the backups, error when trying to add a network location under Windows
* make developer reports working again, set up a script https://bitdust.io/cgi-bin/feedback.py
* changed UDP PING timeout from 10sec to 1 minute
* small fixes in the command line interface


2014-10-15 Veselin Penev [penev.veselin@gmail.com](mailto:penev.veselin@gmail.com)

* fixed error in registration part


2014-10-10 Veselin Penev [penev.veselin@gmail.com](mailto:penev.veselin@gmail.com)

* switched on a new improrved UDP transport - can use UDP to transfer packets now
* upgrade messaging service - safe p2p encrypted chat
* added command line support to send/list messages


2014-08-20 Veselin Penev [penev.veselin@gmail.com](mailto:penev.veselin@gmail.com)

* new tray icons for Microsoft Windows

