const Joi = require('joi')

const OBWriteInternationalConsentResponse6Schema = Joi.object({
	Data: Joi.object({
		ConsentId: Joi.string().min(1).max(128).required(),
		CreationDateTime: Joi.string().isoDate().required(),
		Status: Joi.string().valid('AWAU', 'RJCT', 'AUTH', 'COND').required(),
		StatusReason: Joi.array().items(Joi.string()), // Assuming it's an array of status reasons
		StatusUpdateDateTime: Joi.string().isoDate().required(),
		ReadRefundAccount: Joi.string().valid('No', 'Yes'),
		CutOffDateTime: Joi.string().isoDate(),
		ExpectedExecutionDateTime: Joi.string().isoDate(),
		ExpectedSettlementDateTime: Joi.string().isoDate(),
		Initiation: Joi.object({
			InstructionIdentification: Joi.string().min(1).max(35).required(),
			EndToEndIdentification: Joi.string().min(1).max(35),
			LocalInstrument: Joi.string(),
			InstructionPriority: Joi.string().valid('Normal', 'Urgent'),
			Purpose: Joi.string(),
			ChargeBearer: Joi.string().valid('BorneByCreditor', 'BorneByDebtor', 'Shared'),
			CurrencyOfTransfer: Joi.string().min(3).max(3).required(),
			ExchangeRateInformation: Joi.object({
				UnitCurrency: Joi.string().min(3).max(3).required(),
				ExchangeRate: Joi.number(),
				RateType: Joi.string(),
				ContractIdentification: Joi.string(),
			}),
			DebtorAccount: Joi.object({
				SchemeName: Joi.string().required(),
				Identification: Joi.string().required(),
				Name: Joi.string(),
				SecondaryIdentification: Joi.string(),
			}),
			Creditor: Joi.object({
				Name: Joi.string().required(),
				PostalAddress: Joi.object({
					AddressType: Joi.string(),
					Department: Joi.string(),
					SubDepartment: Joi.string(),
					StreetName: Joi.string(),
					BuildingNumber: Joi.string(),
					PostCode: Joi.string(),
					TownName: Joi.string(),
					CountrySubDivision: Joi.array().items(Joi.string()),
					Country: Joi.string().required(),
					AddressLine: Joi.array().items(Joi.string()),
				}),
			}),
			CreditorAccount: Joi.object({
				SchemeName: Joi.string().required(),
				Identification: Joi.string().required(),
				Name: Joi.string(),
				SecondaryIdentification: Joi.string(),
			}),
			RemittanceInformation: Joi.object({
				Unstructured: Joi.string(),
				Reference: Joi.string(),
			}),
			SupplementaryData: Joi.object(), // Assuming it's an object for additional fields
		}).required(),
		Authorisation: Joi.object({
			AuthorisationType: Joi.string().valid('Any', 'Single').required(),
			CompletionDateTime: Joi.string().isoDate(),
		}),
		SCASupportData: Joi.object(), // Assuming it contains Strong Customer Authentication-related data
	}).required(),
	Risk: Joi.object({
		PaymentContextCode: Joi.string(),
		MerchantCategoryCode: Joi.string(),
		MerchantCustomerIdentification: Joi.string(),
		DeliveryAddress: Joi.object({
			AddressLine: Joi.array().items(Joi.string()),
			StreetName: Joi.string(),
			BuildingNumber: Joi.string(),
			PostCode: Joi.string(),
			TownName: Joi.string(),
			CountrySubDivision: Joi.array().items(Joi.string()),
			Country: Joi.string(),
		}),
	}).required(),
	Links: Joi.object({
		Self: Joi.string().uri(),
		First: Joi.string().uri(),
		Prev: Joi.string().uri(),
		Next: Joi.string().uri(),
		Last: Joi.string().uri(),
	}),
	Meta: Joi.object({
		TotalPages: Joi.number(),
		FirstAvailableDateTime: Joi.string().isoDate(),
		LastAvailableDateTime: Joi.string().isoDate(),
	}),
})

module.exports = OBWriteInternationalConsentResponse6Schema
