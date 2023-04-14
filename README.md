
# Blazor Multiselect Component

I built this component because I found the collection binding to InputSelect tedious.
This component allows you to bind complex types to a simple multiselect.

## PARAMETERS

### TOption Type

    The type for the collection being passed to the component.

### Label string
    
    The text that labels the multiselect input box on the page.

### Options ICollection<TOption>?

    A collection of all of the possible options for the component to display.

### DisplayField string

    The string name of the property to use when displaying the options.
    Preferred way of passing this parameter is by nameof(Model.Property).
    
### SelectedChanged EventCallback<ICollection<TOption>>

    The callback which is invoked whenever the underlying value is updated.

### Selected ICollection<TOption>

    The value that the component holds.

## HOW TO USE

Inside of an EditForm, bind your collection to the BlazorMultiSelectComponent.    

Say we have a product with a list of categories:
```
    class ProductCategory {
        public int Id { get; set; } 
        public string Name { get; set; }
    }
    class Product {
        ...
        public virtual ICollection<ProductCategory> Categories { get; set; } = new List<ProductCategory>();
        ...
    }

    protected List<ProductCategory> AllCategories { get; set; } = new List<ProductCategory>()
    {
        new ProductCategory
        {
            Id = 1,
            Name = "Category 1"
        },
        new ProductCategory
        {
            Id = 2,
            Name = "Category 2"
        },
        new ProductCategory
        {
            Id = 3,
            Name = "Category 3"
        }
    };

    protected Product Product { get; set; } = new Product();
```

Bind it to the component like so:
```
<EditForm>
    ...
    <BlazorMultiSelectComponent.MultiSelect @bind-Selected=@(Product.Categories) Label="Categories" DisplayField=@(nameof(ProductCategory.Name)) Options="AllCategories" />
    ...
</EditForm>
```