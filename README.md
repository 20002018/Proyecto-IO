# Proyecto-IO

#Inputs
turnos_por_dia = 12
q_dominios = 3
q_skills = 2
u_medida = 2 #medida de la celda es de 2 horas
horas_por_turno = convert(Int64, (1/turnos_por_dia)*24)
celdas_por_turno = convert(Int64, horas_por_turno/u_medida) #celdas en excel por turno
turnos_mes= 28* turnos_por_dia 

horas_jornada_regular = 8
horas_minimas_descanso = 12
horas_extras_max = 2
turnos_por_jornada = convert(Int64, horas_jornada_regular/horas_por_turno)
turnos_descanso = convert(Int64, horas_minimas_descanso/horas_por_turno)
turnos_extra = horas_extras_max/horas_por_turno

#Importar data
using CSV
using DataFrames
Demanda = CSV.read("Demanda.csv")
Trabajadores = CSV.read("Trabajadores.csv")

#Estructura de datos de trabajador
mutable struct trabajador
    nombre::String
    sueldo::Float64
    horario_extra::Int64
    skill_dominio::Dict{String,Int64}
    preferencia::String
    prioridad::Int64
    trabajador_asignado::Array{Int64,1}
end

trabajadores=trabajador[]
array=[]
for j in 1:turnos_mes
    new_array=push!(array,j)
    new_array[j]=0
    end
for i in 1:nrow(Trabajadores)
    skill=Dict("Picking"=>Trabajadores[i,:Dominio_Picking],"Calidad"=>Trabajadores[i,:Dominio_Calidad])
   atributos_trabajador=trabajador(Trabajadores[i,:Nombre],Trabajadores[i,:Sueldo_Mensual],Trabajadores[i,:Hora_Extra],skill,Trabajadores[i,:Preferencias],Trabajadores[i,:Prioridad], array)
    push!(trabajadores,atributos_trabajador)
    
end
trabajadores

#Estructura de datos turnos
mutable struct turno
    id::String
    horas::Int64 ##horas por turno
    demanda_skill_dominio::Dict{String,Dict{String,Int64}}
    trabajador_seleccionado::Array{trabajador,1}
    costo_turno::Float64
end
turnos=turno[]
for j in 4:(celdas_por_turno*u_medida)-1 # columnas
for i in 1 # para cada fila 1,2,3,4,5,6
        if Turnos[i,j]>max_valor
            max_valor=Turnos[i,j]
        end
        Demanda1=Dict(Turnos[i,:Skill]=> Dict(Turnos[i,:Dominio]=>max_valor))
        Demanda2=Dict(Turnos[i,:Skill]=> Dict(Turnos[i,:Dominio],Turnos[i,4:ncol(Turnos)]))        
        atributos_turno=turno(Turnos[j,:Skill],)
   
end
   
   
#Imprimir resultados

if Turnos[1,:Skill]=="Picking"
    return angel="Picking"
    angel
    end 
ncol(Turnos)
Turnos
