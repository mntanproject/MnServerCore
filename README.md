# MnServerCore
 MnServerCore
 
 Written in java, planning to use it as android api server. Designed to be light weight.
 Basically its an api rest server, handling user request only via http protocol.
 No method calling implementations yet. Simply routes the server to call class according 
 to request uri.
 
 For example:
 User enters http://localhost:9000/supplier/add
 The web server will call for supplier handler to process the request and response to it.
 method add is Not yet implemented. You can add it if you like and request a commit here :)
 
 Usage:
     
    public static void main(String[] args) throws IOException {
    
    // start server at port 9000
    MnServer server = new MnServer(9000);
    //register route
    HashMap<String,String>routes = new HashMap<String,String>();
    //key supplier is for uri request, value for the server to look for the api processor
    routes.put("supplier","mntanproject.pos.api.SupplierResponse");
    server.getRegisteredRoute().setRegisteredRoutes(routes);
    server.startServer();
    server.shutdownServer();
    System.out.println("Bye...");
    System.exit(0);
    
    }
 
 let me know if you want to extend more or implement the method handling etc ;)
 
 
