```js
    private _isSelected:boolean;

    public get selected():boolean
    {
        return this._isSelected;
    }
    public set selected(value:boolean)
    {
        this._isSelected  = value;
        this.image_selected_icon.visible = this._isSelected;
        if(value)
        {
            this.currentState = "down";
        }
        else
        {
            this.currentState = "up";
        }
    }

```

这个方法不太合理，但是没找到更好的办法，待有空再去处理。