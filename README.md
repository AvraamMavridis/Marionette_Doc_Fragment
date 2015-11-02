# Marionette_Doc_Fragment


Override Marionette's Functions to use DocFragment for appending ChildViews to improve performance on large data sets

```

        /**
         * Overide Marrionete's showCollection to use DocFragment
         *
         * @return void
         */
        showCollection: function(){
          var that = this;
          var ItemView = this.getChildView();

          this._frag = document.createDocumentFragment();

          this.collection.each( function( item, index )
          {
            that.addChild( item, ItemView, index );
          });

          var itemView = {};
          itemView.el = this._frag;
          this.attachHtml( this, itemView, 0 );

          delete this._frag;
        },

        /**
         * Overide Marrionete's renderItemView to use DocFragment
         *
         * @return void
         */
        renderItemView: function(view, index) {
            view.render();

            if ( this._frag ) 
            {
                this._frag.appendChild( view.el );
            } 
            else 
            {
                this.appendHtml( this, view, index );
            }    
        }
```
