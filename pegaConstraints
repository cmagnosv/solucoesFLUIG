/** modelo para usar a função de pegaConstraint
var matricula = pegaConstraint(constraints, "matricula") != 'nao_encontrado' ? getConstraintValue(constraints, "matricula") : '0'; 


/**
 * Pega o valor da Constraint
 *
 * @param {Constraint[]} constraints
 * @param {string} field
 * @returns {string}
 */
function pegaConstraint(constraints, campo) {
   if(constraints !=null){
    for (var i = 0; i < constraints.length; ++i) {
        if (constraints[i].fieldName == campo) {
            return constraints[i].initialValue;
        }
    }
   }
    return "nao_encontrado";
}
#-------------------#
