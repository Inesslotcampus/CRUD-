# CRUD-

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
    
    
    ### View
    
     <form method="post" action="{{ route('backoffice.update', $product->id) }}">

        @method('put')// pas une methode html
        @csrf
        
         <div class="mb-3">
            <label for="exampleFormControlInput1" class="form-label">Name</label>
            <input name="name" type="text" class="form-control" id="exampleFormControlInput1"
                value="{{ $product->name }}">
        </div>
        
        </form>
        
        
        ## Model
        
        
        class Product extends Model
{
    // use HasFactory;

    protected $table = "product";
    protected $fillable = [ "name", "price", "stock" ];  // cathégories que je veux changer 
    public $timestamps = false; // pour eviter erreur column .update
}

        
        
    
    





