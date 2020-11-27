# MnServerCore
 MnServerCore
 
 Written in java, planning to use it as android api server. Designed to be light weight.
 Basically its an api rest server, handling user request only via http protocol.
 No method calling implementations yet. Simply routes the server to call class according 
 to request uri.
 
 uri pattern must be 
 
     // must have api  
     http:// {your server name}/api/{route}/{method}/{parameter}
     
     
 For example:
  
 User enters http://localhost:9000/api/supplier/response/name=mntanproject
 The web server will looked from the pre-registered route supplier and call class 
 based on the route value and its method response(String params) and 
 pass the parameter of string containing name=mntanproject to it.
 In order to pre-register the class so the server can route it, use the following command after create
 the MnServer instance.
 
 
     //register route
     HashMap<String,String>routes = new HashMap<String,String>();
     //key supplier is for uri request, value for the server to look for the api processor
     routes.put("supplier","mntanproject.pos.api.SupplierResponse");
   
 
 in your SupplierResponse class, create a method named response. This method respond 
 must return HttpResponse instance and must accept a String as parameter, otherwise the server 
 will not process the request and API not found will response to user.
 
     public HttpResponse response(String params) {
       response.setContent(params);
       return response;
     }
 
 
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
 
 create SupplierResponse class
    
    package mntanproject.pos.api;
    
    import mntanproject.core.server.response.ContentType;
    import mntanproject.core.server.response.HttpResponse;
    import mntanproject.core.server.response.StatusCode;
    
    public class SupplierResponse  {
      HttpResponse response;
      
      public SupplierResponse() {
        super();
        response = new HttpResponse(StatusCode.OK, ContentType.TEXT, "Response from supplier class");
      }
      
      public HttpResponse response(String params) {
        // do whatever you want with the params processing
        
        //set content in response and return it
        response.setContent(params);
        return response;
      }
    }
   
	 
 let me know if you want to extend more or implements other things to it and etc ;)
 
 
