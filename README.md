# CRUD-


## Create : method create et store

### Route 



Route::resource('product', BackOfficeController::class);


### Controller


public function create()
    {
        $product=Product::all();

        return view('createProduct', compact('product')); //nouveau formulaire à créer
        


        // $input = Request::all();
        // Product::create($input); 
        // return $input;
    }
    
      public function store(Request $request)
    {
        $this->validate($request, [
            'name' => 'bail|required|string|max:255',
            "price" => 'bail|required|int',
            "available" => 'bail|required|int',
            "weigth" => 'bail|required|int',
            "stock" => 'bail|required',
            'description' => 'bail|required|string|max:255',
            "category" => 'bail|required',
            'image' => 'bail|required|string|max:255',
            
        ]);

        Product::create([
            "name" => $request->name,
            "price" => $request->price,
            "stock" => $request->stock,
            "category_id" => $request->category,
            'description' => $request->description,
            "available" => $request->available,
            "weigth" => $request->weigth,
            "image" => $request->image,
            
        ]);

        return redirect(route('backoffice.index'));
    }
    
    
    
## view




## Update: method edit & method update



### Route 



Route::resource('product', BackOfficeController::class);


### Controller



 public function edit(Product $backoffice)
 //doit permettre l'affichage du formulaire
    {

        return view('edit', ['product' => $backoffice]);
    }
    
     public function update(Request $request, Product $backoffice)
    {
    

        $backoffice->update([
        //Ce que l'ont veut changer
            "name" => $request->name,//name vient de input name="name"
            "price" => $request->price,
            "stock" => $request->stock
            
            
        ]);

        

        return redirect(route('backoffice.index'));//ruturn vers mon affichage de formulaire
    }
    
    
    
 ### View (edit)
    
    
    
     <form method="post" action="{{ route('backoffice.update', $product->id) }}">

        @method('put')// pas une methode html
        @csrf
        
         <div class="mb-3">
            <label for="exampleFormControlInput1" class="form-label">Name</label>
            <input name="name" type="text" class="form-control" id="exampleFormControlInput1"
                value="{{ $product->name }}">
        </div>
        
        </form>
        
        
        
### Model
      
        class Product extends Model
{
 

    protected $table = "product";
    protected $fillable = [ "name", "price", "stock" ];  // cathégories que je veux changer 
    public $timestamps = false; // pour eviter erreur column .update
}



## Delect : methode destroy

### Route 

Route::resource('product', BackOfficeController::class);


### Controller

public function destroy(Product $backoffice)
    {

        
        $backoffice->delete();
        return redirect(route('backoffice.index'));
    }
    
### Vue


<form method="POST" action="{{ route('backoffice.destroy', $product) }}">
                        @csrf
                        @method("DELETE")
                            <button type="submit" class="btn btn-danger" value="x Supprimer">Delete</button>
 
 </form>
    
    
    
    






        
        
    
    





