# Confluence Test

  * Please DO NOT fork this project on Github, as we want to be sure candidates' test submissions are original.
  * For unit testing we use XUnit, it is already referenced in the project, but feel free to use which ever framework you prefer.
  * Please create a public repo (GitHub, BitBucket, GitLab etc) and send us the link. Make sure to commit regularly so we can see how you came up with the solution.
  * Remember to be RESTful.

## Portfolio Value Calculator

A big part of what we do at Confluence is work with financial portfolios. As a part of this solution we want to understand how much the entire user portfolio is worth. You will create an endpoint that will allow a user to add stocks to his portfolio (one stock at a time). Your code will need to persist information about these stocks and in return let the user know the total value of his portfolio.


* Create an endpoint so that other services can access the calculation for Portfolio.
* Use this swagger spec as the basis for your API
```yaml
swagger: '2.0'
info:
  title: Portfolio Service
  version: 1.0.0
basePath: /api
schemes:
  - https
paths:
  /portfolio:
    post:
      summary: "Add a new stock to add to the existing portfolio"
      parameters:
      - in: "body"
        name: "body"
        description: "A stock object that needs to be added to the portfolio"
        required: true
        schema:
          $ref: "#/definitions/Stock"
      responses:
        '200':
          description: OK
          schema:
            $ref: '#/definitions/Portfolio'
definitions:
  Stock:
    type: object
    required:
      - name
      - price
      - quantity
    properties:
      name:
        type: string
      price:
        type: number
      quantity: 
        type: integer
  Portfolio:
    type: object
    required:
      - totalValue
    properties:
      totalValue:
        type: number
```

* When a user adds a new stock to the portfolio we need to store information about the stock.
* We need to store: 
  * Name of the stock that is added
  * Price of each individual stock item
  * Quantity of the stock that was bought
* Add an endpoint for this.
* Add validation / error handling you think is appropriate for this endpoint.
* Persist the data. You can store values in an in-memory database (maybe LiteDB), file or any other location you will find appropriate for this implementation.
* Calculate the total value of all items already persisted (if no stocks have yet been added - value of the portfolio is zero) together with value of a stock that is being added now. The portfolio value can be calculated as follows
```
[Stock #1 Price] * [Stock #1 Quantity] + 
[Stock #2 Price] * [Stock #2 Quantity] + 
[Stock #N Price] * [Stock #N Quantity]

For example user adds:
Stock Name: Microsoft; Price: 2.00; Quantity: 3
Your return will be 6.00 

If next user adds 
Stock Name: Google; Price: 7.00; Quantity: 1
Your return will be 13.00 (adding the Microsoft and Google stocks)
```

* Return the total value of the portfolio in the reponse.
* Add appropriate tests and document the endpoint

Thanks for your time, we look forward to hearing from you!
