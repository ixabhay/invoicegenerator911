<template>
<div class="container">
    <div class="row">
        <div class="col-md-2"></div>
        <div class="col-md-8">
            <div class="invoice-box border p-3 m-3">
                <div class="row">
                    <div class="col-md-6">
                        <form id="file-upload-form" class="uploader">
                            <input id="file-upload" type="file" name="fileUpload" accept="image/*" />

                            <label for="file-upload" id="file-drag">
                                <img id="file-image" src="#" alt="Preview" class="hidden">
                                <div id="start">
                                    <div><i class="fa-solid fa-plus"></i> Add Your logo</div>
                                    <div id="notimage" class="hidden">Please select an image</div>
                                    <span id="file-upload-btn" class="btn btn-primary">Select a file</span>
                                </div>
                                <div id="response" class="hidden">
                                    <div id="messages"></div>
                                    <progress class="progress" id="file-progress" value="0">
                                        <span>0</span>%
                                    </progress>
                                </div>
                            </label>
                        </form>
                        <div class="input-group mb-3 mt-3 w-75">
                            <input type="text" class="form-control  invoive-persone" placeholder="Who is this invoice from? (required)" aria-label="Username" aria-describedby="basic-addon1">
                        </div>
                        <div class="row">
                            <div class="col-md-6">
                                <div class="input-group mb-3 mt-3 w-100">
                                    <div class="w-100"><label>Bill To</label></div>
                                    <input type="text" class="form-control invoive-persone" placeholder="Who is this invoice to? (required)" aria-label="Username" aria-describedby="basic-addon1">
                                </div>
                            </div>
                            <div class="col-md-6">
                                <div class="input-group mb-3 mt-3 w-100">
                                    <div class="w-100"><label>Ship To</label></div>
                                    <input type="text" class="form-control  invoive-persone" placeholder="optional" aria-label="Username" aria-describedby="basic-addon1">
                                </div>
                            </div>
                        </div>
                    </div>
                    <div class="col-md-6">
                        <h1 class="invoice-title">INVOICE</h1>
                        <div class="input-group mb-3">
                            <span class="input-group-text" id="basic-addon1">#</span>
                            <input type="text" class="form-control" placeholder="Invoice Number" aria-label="Username" aria-describedby="basic-addon1">
                        </div>
                        <div class="number-list">
                            <div class="input-group mb-3">
                                <label>Date</label>
                                <input type="date" class="form-control" placeholder="Invoice Number" aria-label="Username" aria-describedby="basic-addon1">
                            </div>
                            <div class="input-group mb-3">
                                <label>Payment Term</label>
                                <input type="text" class="form-control" placeholder="" aria-label="Username" aria-describedby="basic-addon1">
                            </div>
                            <div class="input-group mb-3">
                                <label>Due date</label>
                                <input type="date" class="form-control" placeholder="Invoice Number" aria-label="Username" aria-describedby="basic-addon1">
                            </div>
                            <div class="input-group mb-3">
                                <label>PO Number</label>
                                <input type="text" class="form-control" placeholder="Invoice Number" aria-label="Username" aria-describedby="basic-addon1">
                            </div>
                        </div>
                    </div>
                </div>
                <div class="row">
                    <div class="col-md-12">
                        <table width="100%">
                            <thead class="table-head">
                                <tr>
                                    <th width="70%">Item</th>
                                    <th width="10%">Quantity</th>
                                    <th width="10%">Rate</th>
                                    <th width="10%">Amount</th>
                                </tr>
                            </thead>
                            <tbody id="tbody" class="table-body">
                                <tr id="tr-input">
                                    <td><input v-model="decsciption" type="text" class="form-control" placeholder="Description of service or product" aria-label="Username" aria-describedby="basic-addon1" /></td>
                                    <td><input v-model="quantity" type="text" class="form-control" placeholder="" aria-label="Username" aria-describedby="basic-addon1" /></td>
                                    <td><input v-model="rate" type="text" class="form-control" placeholder="" aria-label="Username" aria-describedby="basic-addon1" /></td>
                                    <td>US${{quantity*rate}}.00</td>
                                </tr>
                            </tbody>
                        </table>
                        <div class="p-2"><button v-on:click="addLine" type="button" class="btn btn-success"><i class="fa-solid fa-plus"></i> Line item</button></div>

                    </div>
                </div>
                <div class="row mt-3">
                    <div class="col-md-12">
                        <div class="row">
                            <div class="col-md-6">
                                <div class="input-group">
                                    <div class="w-100">
                                        <lable>Note</lable>
                                    </div>
                                    <textarea class="form-control" aria-label="With textarea" placeholder="Note - any relevant information not already covered"></textarea>
                                </div>
                                <div class="input-group">
                                    <div class="w-100">
                                        <lable>Terms</lable>
                                    </div>
                                    <textarea class="form-control" aria-label="With textarea" placeholder="Term and Condition - late fees, Payment methods, delivery schedule"></textarea>
                                </div>
                            </div>
                            <div class="col-md-6">
                                <div class="number-list">
                                    <div class="input-group mb-3">
                                        <label>Sub Total</label>
                                        <p class="text-right">US${{quantity*rate}}.00</p>
                                    </div>
                                    <div class="input-group mb-3">
                                        <label>Tax</label>
                                        <input v-model="tex" type="number" class="form-control" placeholder="%" aria-label="Username" aria-describedby="basic-addon1">
                                    </div>
                                    <div class="input-group mb-3">
                                         <label>Total</label>
                                        <p class="text-right">US${{taxC()}}.00</p>
                                    </div>
                                    <div class="input-group mb-3">
                                        <label>Amount Paid</label>
                                        <p class="text-right">US${{taxC() + add()}}.00</p>
                                    </div>
                                    <div class="input-group mb-3">
                                        <label>Balance Due</label>
                                        <p class="text-right">US$0.00</p>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <div class="col-md-2"></div>
    </div>
</div>
</template>

<script>
export default {
    name: 'InvoiceVue',
    data(){
        return{
            decsciption:null,
            quantity:null,
            rate:null,
            tex:null
            //amount:this.quantity* this.rate,
        }
    },
    methods: {
        addLine() {
            var trInput = document.getElementById('tr-input');
            var trLine = `
           <tr>
                                    <td><input v-model="decsciption" type="text" class="form-control" placeholder="Description of service or product" aria-label="Username" aria-describedby="basic-addon1"/></td>
                                    <td><input type="text" class="form-control" placeholder="" aria-label="Username" aria-describedby="basic-addon1"/></td>
                                    <td><input type="text" class="form-control" placeholder="" aria-label="Username" aria-describedby="basic-addon1"/></td>
                                     <td>US$0.00</td>
                                </tr>

           `;
            trInput.insertAdjacentHTML("afterend", trLine);
           

        },
        add(){
          var am=  this.quantity * this.rate;
         
            return(am)
        },
        taxC(){
          var am=  this.quantity * this.rate;
          var percent = this.tex * am /100;
            return(percent)
        }
        
        
       
        
    }
    
}
</script>

<style>
/*---------Upload-Logo---------*/
.uploader {
    display: block;
    clear: both;
    margin: 0;
    width: 50%;
    max-width: 300px;
    position: relative;
    overflow: hidden;
}

.uploader label {
    float: left;
    clear: both;
    width: 100%;
    padding: 2rem 1.5rem;
    text-align: center;
    background: #fff;
    border-radius: 7px;
    border: 3px solid #eee;
    -webkit-transition: all .2s ease;
    transition: all .2s ease;
    -webkit-user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    user-select: none;
}

.uploader label:hover {
    border-color: #454cad;
}

.uploader label.hover {
    border: 3px solid #454cad;
    box-shadow: inset 0 0 0 6px #eee;
}

.uploader label.hover #start i.fa {
    -webkit-transform: scale(0.8);
    transform: scale(0.8);
    opacity: 0.3;
}

.uploader #start {
    float: left;
    clear: both;
    width: 100%;
}

.uploader #start.hidden {
    display: none;
}

.uploader #start i.fa {
    font-size: 50px;
    margin-bottom: 1rem;
    -webkit-transition: all .2s ease-in-out;
    transition: all .2s ease-in-out;
}

.uploader #response {
    float: left;
    clear: both;
    width: 100%;
}

.uploader #response.hidden {
    display: none;
}

.uploader #response #messages {
    margin-bottom: .5rem;
}

.uploader #file-image {
    display: inline;
    margin: 0 auto .5rem auto;
    width: auto;
    height: auto;
    max-width: 180px;
}

.uploader #file-image.hidden {
    display: none;
}

.uploader #notimage {
    display: block;
    float: left;
    clear: both;
    width: 100%;
}

.uploader #notimage.hidden {
    display: none;
}

.uploader progress,
.uploader .progress {
    display: inline;
    clear: both;
    margin: 0 auto;
    width: 100%;
    max-width: 180px;
    height: 8px;
    border: 0;
    border-radius: 4px;
    background-color: #eee;
    overflow: hidden;
}

.uploader .progress[value]::-webkit-progress-bar {
    border-radius: 4px;
    background-color: #eee;
}

.uploader .progress[value]::-webkit-progress-value {
    background: -webkit-gradient(linear, left top, right top, from(#393f90), color-stop(50%, #454cad));
    background: linear-gradient(to right, #393f90 0%, #454cad 50%);
    border-radius: 4px;
}

.uploader .progress[value]::-moz-progress-bar {
    background: linear-gradient(to right, #393f90 0%, #454cad 50%);
    border-radius: 4px;
}

.uploader input[type="file"] {
    display: none;
}

.uploader div {
    margin: 0 0 .5rem 0;
    color: #5f6982;
}

.uploader .btn {
    display: inline-block;
    margin: .5rem .5rem 1rem .5rem;
    clear: both;
    font-family: inherit;
    font-weight: 700;
    font-size: 14px;
    text-decoration: none;
    text-transform: initial;
    border: none;
    border-radius: .2rem;
    outline: none;
    padding: 0 1rem;
    height: 36px;
    line-height: 36px;
    color: #fff;
    -webkit-transition: all 0.2s ease-in-out;
    transition: all 0.2s ease-in-out;
    box-sizing: border-box;
    background: #454cad;
    border-color: #454cad;
    cursor: pointer;
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 7em;
    visibility: hidden;
}

/*---------Upload-Logo---------*/
.invoice-title {
    text-align: right;
}

.invoive-persone {
    font-size: 12px;
    padding: 15px
}

.number-list .input-group label {
    padding-right: 5px;
    width: 40%;
    text-align: right;
}
.number-list .input-group p {
    width: 60%;
    text-align: right;
}

.table-head tr {
    background-color: #232e38;
}

.table-head tr th {
    color: #fff;
    padding: 5px 10px;
}

.table-body tr td {
    padding: 5px 5px;

}
</style>
