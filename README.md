<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tax Calculator</title>
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css">
    <script src="https://code.jquery.com/jquery-3.5.1.slim.min.js"></script>
    <script src="https://cdn.jsdelivr.net/npm/@popperjs/core@2.10.2/dist/umd/popper.min.js"></script>
    <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/js/bootstrap.min.js"></script>
    <style>
        .error-icon {
            display: none;
            position: absolute;
            top: 0;
            right: 0;
            margin-top: 8px;
            margin-right: 8px;
        }
    </style>
</head>
<body>
    <div class="container mt-5">
        <form id="taxForm">
            <div class="form-group">
                <label for="age">Age:</label>
                <select class="form-control" id="age">
                    <option value="<40">&lt;40</option>
                    <option value=">=40&<60">&ge;40 &lt;60</option>
                    <option value=">=60">&ge;60</option>
                </select>
                <span class="error-icon" id="ageErrorIcon">&#9888;</span>
            </div>
            <div class="form-group">
                <label for="income">Gross Annual Income:</label>
                <input type="number" class="form-control" id="income">
                <span class="error-icon" id="incomeErrorIcon">&#9888;</span>
            </div>
            <div class="form-group">
                <label for="extraIncome">Extra Income:</label>
                <input type="number" class="form-control" id="extraIncome">
                <span class="error-icon" id="extraIncomeErrorIcon">&#9888;</span>
            </div>
            <div class="form-group">
                <label for="deductions">Deductions:</label>
                <input type="number" class="form-control" id="deductions">
                <span class="error-icon" id="deductionsErrorIcon">&#9888;</span>
            </div>
            <button type="button" class="btn btn-primary" id="calculateBtn">Calculate</button>
        </form>
    </div>

    <div class="modal fade" id="resultModal" tabindex="-1" role="dialog" aria-labelledby="resultModalLabel" aria-hidden="true">
        <div class="modal-dialog" role="document">
            <div class="modal-content">
                <div class="modal-header">
                    <h5 class="modal-title" id="resultModalLabel">Tax Calculation Result</h5>
                    <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                        <span aria-hidden="true">&times;</span>
                    </button>
                </div>
                <div class="modal-body">
                    <p id="resultText"></p>
                </div>
                <div class="modal-footer">
                    <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
                </div>
            </div>
        </div>
    </div>

    <script>
        $(document).ready(function () {
            $('#calculateBtn').click(function () {
                // Clear previous error states
                $('.error-icon').hide();

                // Get input values
                var age = $('#age').val();
                var income = parseFloat($('#income').val()) || 0;
                var extraIncome = parseFloat($('#extraIncome').val()) || 0;
                var deductions = parseFloat($('#deductions').val()) || 0;

                // Validate age
                if (!age) {
                    $('#ageErrorIcon').show();
                    return;
                }

                // Calculate tax
                var tax = 0;
                if (income + extraIncome - deductions > 800000) {
                    if (age === '<40') {
                        tax = 0.3 * (income + extraIncome - deductions - 800000);
                    } else if (age === '>=40&<60') {
                        tax = 0.4 * (income + extraIncome - deductions - 800000);
                    } else {
                        tax = 0.1 * (income + extraIncome - deductions - 800000);
                    }
                }

                // Display result
                $('#resultText').text('Tax to be paid: ' + tax.toFixed(2) + ' Lakhs');
                $('#resultModal').modal('show');
            });
        });
    </script>
</body>
</html>
